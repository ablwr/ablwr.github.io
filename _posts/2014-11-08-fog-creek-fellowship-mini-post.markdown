---
layout: post
title: "Fog Creek Fellowship Mini-post"
date: 2014-11-08 09:04:18 -0500
comments: true
categories: [flatiron, fog creek, gif]
---

I had a great time at Fog Creek getting mentorship from the Trello team but haven't had time to sit down and put it all into words. Fortunately, they say a picture is worth a thousand words.

<!-- more -->

![](/images/fogcreekfellowship_first.gif)

Because this is a vaguely code-focused blog, I must add that one command is worth a thousand seconds screwing around with Photoshop. With ImageMagick, I just ran `convert -delay 20 -loop 0 image*.jpeg fellowship.gif` in each folder of images.

The finest quality .gif is still gonna come out of some dedicated Photoshopping, but this works fine in a pinch.

![](/images/fogcreekfellowship_second.gif)

These gifs are pretty jumbo (despite mediocre quality), which I don't care about but are cruel to slower connections or mobile platforms. ImageMagick can help with that, too, because [ImageMagick](www.imagemagick.org) can do pretty much everything. I mean, it's a wizard.

![](http://upload.wikimedia.org/wikipedia/commons/0/0d/Imagemagick-logo.png)

`convert fellowship.gif -resize 50% fellowship_small.gif` is a quick way to make a smaller copy of an image. There's a zillion other things you can do that I'm not going to go into because the primary point of this post is two simple gifs, but [documentation](http://www.imagemagick.org/script/command-line-options.php) is always your pal, and so is [Stack Overflow](http://stackoverflow.com/search?q=imagemagick).