---
layout: post
title:  "Alfred workflow: Open folder in editor"
date:   2013-07-07 21:40:00
categories: apple alfred
---

![Open a folder in text editor with Alfred](/images/alfred-open-in-editor.png)

Back when I was using TextMate I would make sure to always keep a .tmproj file around for the projects I was accessing frequently. They where a bit of additional cluttler, but it made opening projects from Alfred very easy.

After switching to Sublime Text that kind of workflow wasn't quite as simple out of the box. It would mean doing an Open File... search to find the project's folder, then going up a level and either dragging the folder to Sublime, or using an OS X service that I made in Automator to open the folder in Sublime. Both quick and only a few key strokes, but not as easy as with the project files.

Using an Alfred 2 File Filter in a workflow not only makes this process as easy as it used to be, but there's no longer a need for project files.

Creating a filter with a keyword (in my case "lime") that only searches folders, and then passing the result to an Open File action set for Sublime, everything just works!

<a class="alfred download" href="/alfred/Open-Folder-in-Editor.zip">Download this workflow</a>
