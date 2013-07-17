---
layout: post
title:  "NSUserDefaults best practices and BNUserDefaults"
date:   2013-07-07 22:40:00
categories: apple iOS
---

Something I've noticed, after working on several of my own apps, dealing with existing apps at work, and looking at open source and example code, is that every has their own take on handling `NSUserDefaults`.

<iframe src="http://ghbtns.com/github-btn.html?user=Bitnock&amp;repo=BNUserDefaults&amp;type=watch&amp;count=true&amp;size=large" allowtransparency="true" frameborder="0" scrolling="0" width="179" height="30"> </iframe>

I suspect this is largely because `NSUserDefaults` is a fairly straight-forward API once you know how it works. Even though it requires some boilerplate, it's not enough to motivate improvement.

At some point in the last few months, though, I realized I was working on three different projects that I mostly was responsible for myself, and even they did defaults and settings a bit differently. It's not like switching between them caused any problems, but it was noticeable. Not a red flag, but maybe a yellow flag?

After trying a few different things, I landed on a system that I think makes some good progress. First, it clarifies the somewhat ambiguous and confusing naming conventions that are part of `NSUserDefault`'s standard API. Second, simply by having a standard it's marginally easier to keep things organized in a team setting. Lastly, it does provide some useful default functionality and reduces boilerplate and the risk of screwing things up.

### Always use constants

I've seen a lot of examples of people using strings directly as the keys they're passing into the setters and getters. There's nothing necessarily wrong with this, but it more often than not means you're trying to track down the correct string in other parts of your code so everything matches and works correctly.

Using constants everywhere means you can rely on code completion. It prevents mistakes from mistyping a key value, and makes it easier to get a list of all available defaults without having to hunt them down.

In addition to just using constants everywhere, I've also standardized on the naming convention of those constants. Take, for example, an app with the prefix `AB`. I would always use keys called `ABUserDefaultsKeyVersionString`, `ABUserDefaultsKeyLaunchCount`, or `ABUserDefaultsKeyPlaybackRate`. A little verbose, but there's no confusion.

Finally, the value of these constants should simply be their own name. Eg: `@"ABUserDefaultsKeyLaunchCount"`. That means when you're referencing defaults from a settings bundle, everything matches up.

### BNUserDefaults

I found the most annoying part of `NSUserDefaults` to be registering the default values. This is another place where apps and people did things quite differently. Some handled it in the app delegate, some in the root view controller, and others had a separate class or manager.

In reality, 99% of the time the way this registration should happen is very predictable. It needs to happen once, before any of values are touched on the `standardUserDefaults`. The app delegate may feel like a good place for that, but we can do better.

It will require a separate class, though. Having a standard wrapper is better than coming up with a new solution for every new app I think, so it's not that bad.

[BNUserDefaults](https://github.com/Bitnock/BNUserDefaults) is the wrapper that I've come up with. It does very few things, and is intended to be subclassed.

The first thing it does, is provide a standard place to define default values. By overriding the `defaults` method in your subclass, you can return a dictionary of all your default values.

The next thing it does is register those default values when the class gets initialized. That means we know all our defaults are up to date before any of the values in the store get changed. Additionally, the `initialize` method of our subclass is a great place to handle any other tasks related to settings and defaults that you want to deal with automatically.

I almost have a defaults to store a string value of the app's current version (version number, build number, build configuration, etc). Having it as a default means I can display it in the settings bundle. I always want it to be up to date, though, and it only needs to be updated once each run, so inside `initialize` takes care of that.

`BNUserDefaults` also provides a `settings` method, to try to disambiguate some of the data that is associated with `NSUserDefaults`. The fact that the current values are called defaults, but there are also *default* defaults sometimes isn't obvious at first. Accessing `standardUserDefaults` through `settings`, I find, makes things more clear and readable.

Finally, having this class as a standard part of my new app template means I always have a good spot to stick the miscellaneous methods I end up needing for keeping track of various bits of data. Incrementing launch count, updating the current view to launch to, etc. There's no more guessing where that will take place.
