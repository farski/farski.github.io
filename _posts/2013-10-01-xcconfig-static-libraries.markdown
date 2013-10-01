---
layout: post
title:  "Linking static libraries in a .xcconfig"
date:   2013-10-01 01:10:00
categories: apple iOS
---

There are many reasons why you may choose to use configuration files (.xcconfig) to manage the build settings of a project. Recently I've been working on a that has many targets, but except for the name and info plist file, every other build setting was identical. This is a scenario where a single xcconfig file can make maintaining a suite of apps significantly easier.

One of the trickier things to move out of the settings for the individual targets and into the configuration file was the libraries. Normally found under the **Build Phases** tab of a Target, frameworks and libraries can be added and removed from the **Link Binary With Libraries** panel. Having several identical targets would mean making sure every library and framework were added every target by hand, if there weren't a way to centralize that setup.

Moving frameworks to an xcconfig file is fairly straight forward. For each framework your app needs to link against, you will add a `-framework` flag to the `OTHER_LDFLAGS` declaration. This works for both native frameworks as well as third-party frameworks. To make sure your third-party frameworks behave properly, you will likely also need add them to your search paths, which can also be done in the configuration file.

An example using some commong frameworks may look like this:

    FRAMEWORK_SEARCH_PATHS = $(inherited) "$(SRCROOT)/Vendor/HockeyApp/HockeySDK.embeddedframework" "$(SRCROOT)/Vendor/Crashlytics"
    OTHER_LDFLAGS = $(inherited) -framework CoreText -framework AdSupport -framework CoreVideo -framework CFNetwork -framework HockeySDK -framework Crashlytics

Each framework is simply listed as a separate `-framework` flag. This would be equivalent to having those six frameworks listed in the **Link Binary With Libraries** panel in your project settings.

You can also move any libraries you use into the xcconfig file as well. Libraries that are included in the iOS SDK (such as libz, libxml2, and libsqlite3) are as easy to add as the frameworks. You declare each with a `-l` flag. These are also added as `OTHER_LDFLAGS`. Adding them to the previous example would result in the following:

    OTHER_LDFLAGS = $(inherited) -framework CoreText -framework AdSupport -framework CoreVideo -framework CFNetwork -framework HockeySDK -framework Crashlytics -lz -lxml2 -lsqlite3

Note that the `lib` prefix of the library names is dropped. The space between the `-l` and the name is optional.

Things become a bit more complicated when dealing with third-party static libraries. Using Google Analytics as an example, you'll need to do three things to get an xcconfig file to manage the static library that Google offers. Firstly you'll want to ensure that the library is in your search paths, which can be done with `LIBRARY_SEARCH_PATHS`. Then you will need to add flags for both the location *and* the library itself. This is done by using the `-L` and `-l` flags, respectively. For our example project, that would result in an xcconfig file of:

    FRAMEWORK_SEARCH_PATHS = $(inherited) "$(SRCROOT)/Vendor/HockeyApp/HockeySDK.embeddedframework" "$(SRCROOT)/Vendor/Crashlytics"
    LIBRARY_SEARCH_PATHS = $(inherited) "$(SRCROOT)/Vendor/Google Analytics"
    OTHER_LDFLAGS = $(inherited) -framework CoreText -framework AdSupport -framework CoreVideo -framework CFNetwork -framework HockeySDK -framework Crashlytics -lz -lxml2 -lsqlite3 -L"$(SRCROOT)/Vendor/Google Analytics" -lGoogleAnalyticsServices
    
