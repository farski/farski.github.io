---
layout: post
title:  "Blending modes in javascript"
date:   2012-02-19 12:00:00
categories:
---

I spent quite a while today trying to get the core set of blending modes to behave the same way in javascript as they do in Photoshop. There are only a handful of actual code example results on google, and a lot of them just…don’t work. Even the wikipedia page wasn’t terribly helpful. Finally, though, I got them all working. A few differ from PS a bit, but that may just be a color space thing when I was comparing them side-by-side.

These should read pretty easily. They handle a single color channel at a time (so some of the more complex modes wouldn’t work this way, eg if they need to convert the entire pixel the HSL). Base is the bottom layer color value, and adj is the top layer.

{% highlight javascript %}
var blenders = {
  normal: function(base, adj) { return adj; },

  darken: function(base, adj) { return Math.min(base, adj); },
  multiply: function(base, adj) { return ((base * adj) / 255); },
  colorburn: function(base, adj) { return adj <= 0 ? 0 : Math.max(255 - ((255 - base) * 255 / adj), 0); },
  linearburn: function(base, adj) { return Math.max(0, (base + adj - 255)); },

  lighten: function(base, adj) { return Math.max(base, adj); },
  screen: function(base, adj) { return (255 - (((255 - base) * (255 - adj)) / 255)); },
  colordodge: function(base, adj) { return adj >= 255 ? 255 : Math.min(base * 255 / (255 - adj), 255); },
  lineardodge: function(base, adj) { return Math.min((base + adj), 255); },

  overlay: function(base, adj) { return (base < 128) ? ((2 * base * adj) / 255) : (255 - (2 * (255 - base) * (255 - adj) / 255)); },
  softlight: function(base, adj) { return (base < 128) ? (((adj>>1) + 64) * base * (2/255)) : (255 - (191 - (adj>>1)) * (255 - base) * (2 / 255)); },
  hardlight: function(base, adj) { return adj < 128 ? (2 * base * adj) / 255 : 255 - ((2 * (255 - base) * (255 - adj)) / 255); },

  difference: function(base, adj) { return Math.abs(base - adj); },
  exclusion: function(base, adj) { return 255 - (((255 - base) * (255 - adj) / 255) + (base * adj / 255)); },
  subtract: function(base, adj) { return Math.max((base - adj), 0); }
};
{% endhighlight %}

There are a few more easy ones I need to get to still (vivid light, etc). And then I may try to do the harder ones.
