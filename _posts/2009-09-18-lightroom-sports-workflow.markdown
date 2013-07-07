---
layout: post
title:  "Lightroom post-production workflow"
date:   2009-09-18 12:00:00
categories:
---

Thanks to tools like Aperture and Lightroom, what happens to photos after they come off the flash card is now much more predictable than in the past. Whereas it used to be that just about everyone had a different way of organizing their digital negatives, choosing formats, keeping track of originals and edits, and doing all the other things that need to be done to get a final product out the door, these types of applications have adopted a convention-over-configuration attitude. Even though lots of little choices are being made by the software, in general they’re making them in a transparent way, and still leaving some of the specifics up to the user.

It’s not to say that as soon as you choose Lightroom instead of Aperture you’re stuck with one workflow for the rest of your life. There’s plenty of flexibility built in so you can do things one way for the weddings you shoot, and a completely different way for managing your family Christmas snapshots. The niceties that you don’t have control over are the things like catalog metadata management and handling multiple versions of a single photo; things you probably don’t want to be dealing with anyway.

I’m going to go over just one workflow, that I commonly use for dealing with sports photography, but it is basically destination agnostic and could probably work well for any workflow that starts with a large volume of images coming in at one time. I will talk a bit about how I manage my files on the hard drive, the ways I use various features of Lightroom, and some of the custom conventions I have decided on that help me get things done.

## File management

I use a very simple solution for keeping track of images on my hard drive. Inside an Archive folder, I have a separate folder for each year, and one extra folder called Singles. Singles is used to keep hold things like photos I take with my cell phone, a shot of the sunset I took while at a football game that I don’t want in the same place as those sports images, etc. Within each year-specific directory, I don’t do any further subdividing to hold individual folders of images. Even if a single year ended up with 200 different child folders that would be easy enough for me to handle, given how infrequently I am actually dealing with these folders and files in the Finder itself.

As much as I try to stick to conventions for things I do on computers, naming the specific folders is one area where I say “whatever works” is better than trying to live within a specification (even if it were my own). Each folder name begins with a date (2009-09-18, for instance) and then a brief description of the event. With sports I almost always put some indicator of the sport right after the date (TF, Soccer, etc)  and then a description of the event. Sometimes I will use “TeamA @ TeamB” notation, and other times I’ll say “TeamB vs TeamA”; whichever team is more important to me I’ll put first (if I’m getting paid by or just covering one team, for instance).

I will get all my files organized in their original raw format, and then at some point get them converted over to .dng. There are plenty of other places were the merits and possible caveats of that format are discussed, so I won’t go into them here, but it works well for me. I do not include the original raw file in the negative when I make the conversion.

I will say that while this setup works perfectly fine when browsing my archive in the Finder, even with a single year having many many events, since the list in Lightroom directly matches the folder structure, once you get more than 30 events in a single year scrolling does become an issue. I have thought about breaking years down into quarters just to help reduce scrolling for the times I need to go back and forth between events, but that doesn’t happen too often, so as of yet I haven’t.

## Lightroom

### First phase

When I’m adding a new folder to Lightroom, I don’t do too much in terms of adding presets or metadata during import. I will add some IPTC copyright info, and a basic set of keywords, but that’s about it. There are only a few venues that I have specific develop presets for, and even then sometimes I will just start the developing from scratch to eliminate the risk of all my shots from different days and different events looking the same.

Since I’m usually coming home with between 700 and 1,200 images, letting LR generate large previews for every shot can be time consuming, and even just leaving that process running in the background, I find, slows what I’m actually trying to do down too much. So I will cancel that process unless I really have lots of time to kill before getting to work.

### Second phaes

Now I start the most mundane part of my workflow: going through each shot one by one and making some initial decisions. I find that without waiting for a full-size preview, or even a minimal preview, to render, I can save loads of time marking some shots as ‘rejected’ from just the super-pixellated preview that first comes up with I select a new image. I’m not trying to save time at the expense of making mistakes, so if there’s any question about what the photo will look like I’ll wait the two or three seconds for the full render to come up, but not waiting to mark maybe the 25% of images that are completely out of focus, have a ref passing in front of the camera, or are just obviously not up to snuff is a huge bonus.

During this first run through of all the images, I will mark rejects, as I just talked about, and mark any shots that I think have potential of being delivered as ‘picks’. Even if I have a 10-shot sequence of the same moment during a game, at this point I may pick four or five of them that I like. During this process I don’t like going backwards at all, so if I see one shot and pick it, and get to the next one and say “oh this one’s better” I’ll just pick it and move on, I won’t backtrack and un-pick the first one.

I will also say I don’t like using auto-advance, which in Lightroom will move from one shot to the next as soon as you flag it. Sometimes I get a little trigger happy and hit P instead of X, and when it moves automatically I find I catch those errors less often. Also, when you want an image to remain unflagged (which is most images in a set of 700, for me, from a game), then you have to hit the U key to unflag a photo that didn’t have a flag to begin with. I do wish there were some set of keys on the keyboard that had Reject/Unflag/Pick physically next to each other, but until that happens I will stick with using the arrow keys to advance.

### Third phase

Once I reach the end of the photos, I delete (from disk) all my rejects. It’s probably a good idea to give them a once over before you actually hit delete just to make sure nothing you wanted slipped in, but I like getting them out of the way early; less chance they get bulk-selected by accident at some point and I waste time waiting for a couple hundred extra images to convert to dng or apply some metadata.

Now I filter down to just my picks and really start making decisions; it’s also where I start using color labels to help organize things even further, so I’ll spend a second talking about those.

### Color labels

The color label set I use for almost all my sports post-production is called my “Mass-ingest workflow” custom color label set. It works well with any large volume of photos that are being whittled down considerably to a select group of deliverables. From Red to Purple the labels are: Reevaluate, Correct, Finalized, Export, and Special consideration. They are pretty self-explanatory, but some of the thinking behind them is that each is pretty much mutually exclusive, so there’s never any overlap, and, except for green/finalized, they are temporary; I don’t really like having my library look like a rainbow. These labels are not set up as a progression; most images will never be red/reevaluate or special consideration. They are just there if I need them and they can help move things along.

I should mention that Export and Finalized do pretty much always overlap, but I use blue/export just-in-time when I’m actually getting ready to move some files out of LR. So, for instance, of 35 finalized (green) picks from an event, I may only want five to put online. I will go through and select those five by switching them over to blue, export, and then immediate switch them back to green. If that collection of photos needs to be retained more permanently, I will make…a collection!

Ok so back to the workflow, as I review the picks, I will look at individual images and either unflag them in I am certain they’re unusable, mark them as red/reevaluate if I’m still undecided, or mark them as yellow if I know I want to spend time editing them. For the shots from a single sequence, I will see which one is the best and, almost always, unflag the others. Every so often multiple shots from a single sequence make it through.

### Fourth phase

Once I have everything set as either yellow or red (I know it seems like I spend a lot of time color-coding images, but it’s really just making a decision I would be making otherwise more visual, I’m not really spending any extra time to make sure my colors are correct) I will start to develop. Most times I can come up with a set of base develop settings for the entire event, or at least a large chunk of the event, that I can apply to lots of images as I go and just make some small tweaks to. I’ll copy that set of settings (not make a preset, since I’m generally not reusing these settings for other events), and as I make the image specific fixes (crop, straighten, spot corrections, etc) I’ll just command+shift+v and make any changes I need, usually to exposure or sharpening.

Most times the games I’m covering are in the afternoon and outside, so the lighting conditions are changing quite a bit from beginning to end. In those cases I’ll develop a couple shots from the beginning, a couple from the middle, and a couple from the end, and use those three different base settings to work with the remaining shots. Otherwise I find myself trying to use settings from an early (sunny) shot to start working with a shot from later in the game and realize that it’s very tough to get things right by making lots of little tweaks; it’s better to just force yourself to start from scratch and develop specifically for that shot to get the best results.

Now is probably a good time to mention that if I come across I shot that I want to include in my deliverables for a given job, but also want to go back to later and maybe try as a black and white or some other process that isn’t appropriate for the client, I’ll mark it as purple/special consideration. Sometimes I’ll actually make a virtual copy and set that to purple, but either way I just want to remember to go back and try something with that shot.

At this point I should be getting pretty close to having all green/finalized images. It’s time to make final decisions on any red/reevaluate photos I still have lingering around, and any editing (yellow) that I had been putting off, maybe because I needed to actually bring the shot into Photoshop, or spend a lot of time making spot corrections. Once I’ve got green across the board, I can do whatever it is I need to with the images that made the last cut: export to the web, print, prepare for inclusion on a DVD, etc. I’ve already talked about how I use my blue label to help with that.

Someone reading this is probably thinking “don’t ‘pick’ and ‘green’ mean the exact same thing at this point?” Yes, in most cases they do. And to be honest, a most times if I have a folder of images and the only color label being used in it is green, I will just unset them and rely on their flag status to let me know which ones I like (remember, I said I don’t like having colors in my library). If I’m doing something more long-term, like building one set of images that will be printed, and a different set going to DVD, I may even start re-using the color labels for arbitrary selections that don’t match their label. But eventually, I will almost always remove all the colors.

### Clean-up

Once I’m done editing and all my images are ready to ship whenever the need arrises, I’ll do some last minute clean-up. I will go through and make sure my IPTC data is complete, I will do a more specific round of keywording (instead of just ‘soccer’, I will add ‘goalie’ to the appropriate shots), and maybe even go through and delete (from disk) some more of the unflagged shots that are just a little soft, or I know that in a million years I’m never going to need. In general, though, I save all the images I don’t actual deliver. Space is cheap, and it’s not really worth my time to risk deleting an image and then later realizing it was the ONLY shot of #18 for that whole game and regardless of how boring it is you still need to print it out.

Generally I won’t rate any images (with stars) at this point. Unless I think the shot is THE BEST EVER!! I would rather wait a week or so and look at the whole set again later, or get some outside feedback before I start saying some shot is in the real top tier of all my shots. Even then I will start every image out at one star and over time increase it if I feel it’s necessary. Such a small percentage of all my shots have any rating at all that it really doesn’t matter too much what the actual value is. Doing a quick star filter gives me a nice, small sampling of exceptional shots.

That is a pretty complete run-through of just about every sports event I process. I’ve used a very similar process to end up with two shots for a single client, and also 1,000 shots that I used to create a stop-action video. Like all workflows, it’s a very personal thing, but I think Lightroom does a good job of limiting the number of ways that you can rate and organize, while letting everyone do things the way that best works for them. If you’re even a little familiar with Lightroom, you should be able to understand how I’m using this system and hopefully why, and maybe it can help you work a little more efficiently in your own endeavorers.
