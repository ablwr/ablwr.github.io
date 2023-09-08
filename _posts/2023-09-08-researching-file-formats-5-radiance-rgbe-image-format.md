---
layout: post
title: "Researching file formats 5: Radiance RGBE Image Format"
date: 2023-09-08 09:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

This format was one that I started researching, but was only accidentally part of the set I was given, so this one will never have an FDD! But I learned a bit about the format before that was determined, so it merits having a blog post anyway.

Radiance RGBE Image Format: This looks to be the first popular HDR image storage format.

I came across these incredibly sick book covers and equally powerful book series website that is still being kept up to date called [GRAPHICS GEMS](https://www.realtimerendering.com/resources/GraphicsGems/)!  Love when I can buy a book or get all the contents online for free! (Shamelessly I must add that if you like that too, you can see or buy my audio/film/video formats series by visiting the [Media Guides Series website](https://mediaguides.archivesoftomorrow.com/)!)

New word for me:
"mantissa"
Use it in a sentence, why dontcha? Okay: "The basic idea is to store a 1-byte mantissa for each of
three primaries, and a common 1-byte exponent" (from the spec: [https://radsite.lbl.gov/radiance/refer/filefmts.pdf](https://radsite.lbl.gov/radiance/refer/filefmts.pdf))

The computing definition: "the part of a floating-point number that represents the significant digits of that number, and that is multiplied by the base raised to the exponent to give the actual value of the number."

Another new word for me:
["metamerism"](https://en.wikipedia.org/wiki/Metamerism_(color))
"a perceived matching of colors with different (nonmatching) spectral power distributions"
Sometimes you know the concept but not the word behind it.

And sometimes I feel like I've been able to understand a lot about color spaces while still understanding basically nothing about color spaces.

Maybe working on this I'll finally understand ray-tracing.............. I dunno.

There are at least two versions of this format, so it could be considered a family rather than just one format.

While researching, I got to enjoy [these photos taken during SIGGRAPH 2002](http://anyhere.com/gward/snaps/SG02/index.html), among others. They are just normal image files though, not RGBE files. Still, glad people were having a good time.

Are you here because you need sample files? Here you go:
- [https://radsite.lbl.gov/radiance/pub/pics/index.html](https://radsite.lbl.gov/radiance/pub/pics/index.html)
- [https://telparia.com/fileFormatSamples/image/radiance/](https://telparia.com/fileFormatSamples/image/radiance/)
- [https://pfstools.sourceforge.net/hdr_gallery.html](https://pfstools.sourceforge.net/hdr_gallery.html)
