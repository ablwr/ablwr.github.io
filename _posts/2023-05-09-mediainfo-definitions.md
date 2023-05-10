---
layout: post
title: "Mediainfo Definitions"
date: 2023-05-09 09:00:00 -0500
tags: [mediainfoinfo, small projects, webdev]
---

![MediaInfo Definitions](/images/mediainfo-definitions.jpg)

This is a delayed blog post from a [project I threw together back in March](https://github.com/ablwr/mediainfo-definitions).

That project was: [Mediainfo Parameter Definitions](http://bits.ashleyblewer.com/mediainfo-definitions/)!

See, I had done a lot of work three years ago, [working in the open right here on this blog, in fact](https://bits.ashleyblewer.com/blog/2020/01/10/mediainfoinfo-initialize-project/), around providing definitions to the potential parameter options in [MediaInfo](https://mediaarea.net/MediaInfo).

After three years, that work was finally merged in the library! But also, it wasn't added to the library at the same time! Because documentation was being extracted from the core package, for size reasons. But the definitions still live (refreshed) in the core codebase, just not distributed as part of the package. Anyway, I was excited about this so I wanted to showcase the work that I did, and I made a small website to do that.

The issue with just having all of the definitions living as a table is that there are just too many of them. Several thousand HTML elements on the page is pretty brutal. Computers are funny, and it's funny how you can easily handle a lot of data existing on the client side of the browser, but showing it all will weigh it down quickly.

The site is plain HTML/CSS/JS, my favorite way to work. I used [PapaParse](https://www.papaparse.com/), my favorite library for quickly parsing.

To help show all of the data for browsing without hurting the browser, I used [Clusterize](https://clusterize.js.org/).

You can browse everything, do an exact string match for the parameter you're likely seeing on your screen, and you can narrow down by Stream category (Audio, Video, Text, et al).

![MediaInfo Definitions - results for Codec](/images/mediainfo-definitions2.jpg)