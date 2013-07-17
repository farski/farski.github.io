---
layout: post
title:  "BNRSSFeedParser and iOS7"
date:   2013-07-08 01:10:00
categories: apple iOS
---

`BNRSSFeedParser` is an RSS feed parser that I wrote for one of my apps. It provides a very low friction way of taking the URL of a feed and getting back an object with that feed and its items or entries. All of the HTTP handling and XML parsing is taken handled behinds the scenes.

One assumption the library makes is that most of the time you will parsing a feed that you have seen before (ie, an update). To handle those situations, the parser accepts two argument: an Etag and a date. The Etag is used to prevent unnecessary network traffic when a feed hasn't been changed. The date acts as a kill-switch for the XML parser; once an item in the feed prior to the date has been reached, the parser stops parsing and assumes you already know about the rest of the data.

One of the new APIs in iOS 7 that many apps which do feed parsing will likely take advantage of is **background fetch**. Unlike previous versions of the OS, where you were limited to running your code only when your app was open, or for a few minutes after it went into the background, background fetch allows you to register your app for periodic arbitrary task execution.

Even if you app is closed, as long as it has been registered for background fetch, the OS will wake it up and run some code. This is great news for apps that utilize data from RSS feeds, since it will be possible to have your local data sync up with the feed before the user comes back to the app.

Since `BNRSSFeedParser` has been intended to handle the most common update scenarios in the past, providing native support for background fetch only makes sense. It will likely become the default method of updating data in apps within the first few months after iOS 7 is released.

### What's required

Implementing background fetch in an app is relatively simple. There's a new callback on the app delegate that will get called when the app is woken up by the background scheduler. In there you are essentially free to put any code you want, but there are still some limitations placed on your app's execution while in the background. In order to ensure that the result of the fetch is what you anticipate, there are some considerations to be aware of.

For one, your app will still be killed after some amount of time. Because of how iOS 7 coalesces network activity, very long running requests or jobs may simply not finish. As such, what you choose to execute in the fetch callback should finish relatively quickly.

Along those same lines, the jobs you are running periodically in the background are not intended to download media. That is to say, if you are updating podcast feeds in the background, you shouldn't also be trying to download the MP3s for new episodes as part of the background fetch. There are better ways to handle that, which will be mentioned later.

The last major change required to handle background fetch is `NSURLSession`. This is a new API that supplements `NSURLConnection`, but offers support for background jobs.

### Changes

The biggest change to `BNRSSFeedParser` is adopting `NSURLSession`. Because `AFNetworking`, the library that was being used to make the HTTP requests (and also partly handle XML parsing), is based on `NSURLConnection` it is not sufficient for handling background updates.

While the `NSURLSession` API is not as friendly as `AFNetworking`, it is much more similar when compared to the old API. Requests are made with blocks to handle the result, which will be familiar to users of `AFNetworking`. Lacking is the ability to detect content types and return pre-parsed JSON or XML that is ready to be parsed. Instead you always get back `NSData`.

That being said, the changes required in `BNRSSFeedParser` were pretty minimal. `AFNetworking` has been removed entirely, and two new classes are shipped with the library. One is an `NSURLSessionConfiguration` that has a `requestCachePolicy` suitable for the standard use case of the library. The other is a `BNRSSFeedURLSessionManager`, which create and maintains an `NSURLSession` using that configuration, through which the actual HTTP requests will be made.

### Implementation

Upgrading to the new version of `BNRSSFeedParser` should require very few implementation changes. The `parseFeedURL:` method hasn't really changed. Using the new version, though, ***requires*** iOS 7. It maintains no backwards compatibility for iOS 6. It would not be difficult to rework the library to use `NSURLSession` if available, or fallback to `AFNetworking` when necessary.

One implementation detail that will likely be required is a more explicit handling of changes to your local data when doing bulk updates in the background. The app delegate callback for background fetch expects a `completionHandler` to be called when the fetch is done, with either `UIBackgroundFetchResultNewData` or `UIBackgroundFetchResultNoData` being passed in.

Determining whether new data was found during parsing could take several forms, and will depend on how your code currently handles multiple calls to `BNRSSFeedParser`. Likely there is a callback or block executing every time an individual feed is completed during the batch.

When executing that block inside the background fetch callback in the app delegate, you will want to keep a running tally of how many items are being returned with `BNRSSFeed` object. If none are, you will know that the update for that feed yielded no new items. If at the end of the batch the total is still 0, it is probably safe to assume you can pass `UIBackgroundFetchResultNoData` to the `completionHandler`.

(This method ignores any changes to feed data that resulted from the parsing. For example, if a feed's title changes. Relying on the item count means your UI may be slightly out of date when the app is foregrounded. A more complex method of tracking changes would be necessary to avoid that.)

As mentioned previously, should the result of these updates be a need to download media, those tasks should **not** be handled by the background fetch. Instead, those requests should be handled by a separate `NSURLSession` that was created with a `backgroundSessionConfiguration:` identifier. That session is something your own app code should take care of.

Tasks for background sessions are handled by the OS independently of background fetches, and are allowed to continue over longer periods (though not necessarily uninterrupted). Background fetches work in conjunction with jobs scheduled through a background session, but they are fundamentally different.

Even if you don't make those changes, and continue to download media only when your app is in the foreground, making these few simply changes to how `BNRSSFeedParser` is implemented will allow you to at least take advantage of background fetch for data updates as soon as iOS 7 is available.

Apple recommends registering your app for background fetches as frequently as possible (`UIApplicationBackgroundFetchIntervalMinimum`). This is not a specific amount of time; the scheduler tries to intelligently perform fetches when it makes sense. If your app is opened in the morning and evening, background fetches won't occur frequently during the middle of the night and around lunch time.

Background fetch registration is not handled by `BNRSSFeedParser`; your app must do that in addition to setting up the callback on the delegate.
