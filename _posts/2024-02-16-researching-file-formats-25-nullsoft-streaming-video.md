---
layout: post
title: "Researching file formats 25: Nullsoft Streaming Video"
date: 2024-02-16 07:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

"Support for more codecs will be added soon." -- [Nullsoft, 2004](https://web.archive.org/web/20040715015529/http://www.nullsoft.com/nsv/)

Last week was an audio codec, this week is an audio/video container. (See [my training site](https://training.ashleyblewer.com/) for nuances there,if needed!)

And it's a container for streaming media!

If you've heard of Nullsoft before, it's probably because they made Winamp. If you've used [Winamp](https://en.wikipedia.org/wiki/Winamp)... you are old. I don't know what else to tell you. 

Anyway, NSV is interesting, and I'm not just saying that because I was a [huge Llama-head](https://gizmodo.com.au/2013/11/a-brief-history-of-the-winamp-llama/) back in the 2000s. Or maybe I am. I don't know, this is my blog, I can say what I want! In general, the format and Winamp were tightly linked together, authored by the same people, and were used together, although NSV didn't have to exclusively be used with Winamp, and it wasn't. It was also tightly linked to another Nullsoft product, Shoutcast. Nullsoft was bought by AOL pretty early on, so it was used in some AOL products as well. AOL sold off Winamp/Shoutcast and essentially Nullsoft [in 2014](https://techcrunch.com/2014/01/01/aol-sells-winamp-and-shoutcast-music-services-to-online-radio-aggregator-radionomy/).

There's also an NSV-inspired format called STARDIVA that I learned about while working on this project. It's also on the Digital Preservation Coalition's BitList as an example of an endangered format, you can [read what they have to say here](https://www.dpconline.org/digipres/champion-digital-preservation/bit-list/endangered/bitlist-legacy-video-files), at the bottom as "Case Study".

The format comes with an optional header (polite to include, but no worries if not, sorta -- it can hold a table of contents though), and then data. It was important for someone to be able to jump to any part of the stream and start from there without having to buffer any of the previous data, since the point is streaming.
