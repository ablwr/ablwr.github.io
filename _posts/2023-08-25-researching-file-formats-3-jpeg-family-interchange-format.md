---
layout: post
title: "Researching file formats 3: JPEG File Interchange Format Family"
date: 2023-08-25 09:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

As a meta-update: The formal works are starting to appear online! [Go here](https://www.loc.gov/preservation/digital/formats/fdd/fdd_workplan.shtml) to see Set 9's official format descriptions. I've updated the previous two blog posts with direct links. Going forward, I thiiink my blog posts will mostly, if not completely, run ahead of the published sets. But if they don't, I'll lead with the links (because that's where the useful info is, instead of these blog posts which are more like the Hot Takes Department).

JFIF. Have I heard of this format family before I started working on this project? No. Do I use this format every day, multiple times a day? Yes!!!

That's probably embarrassing for me to admit, but I don't care! I've never thought about JFIF (JPEG File Interchange Format), I just lumped it all into the category of JPEG. 

Here's all you need to know:
**"JPEG is the codec, JFIF is the file format."**

From 2019 and still excellent, here's a longread and interactive site all about the JPEG that I used to assign when I taught grad students: ["Unraveling the JPEG"](https://parametric.press/issue-01/unraveling-the-jpeg/)

It was funny to read the SPIFF file format section in the [Encyclopedia of Graphics File Formats](http://fileformats.archiveteam.org/wiki/Encyclopedia_of_Graphics_File_Formats) (I'm lucky enough to have a hard copy!), because it talks a big game about how SPIFF is _THE_ JPEG file format and how JFIF sucks ass, actually, and SPIFF is the hot new thing, because that format clearly went nowhere. I can't wait for a 10-part miniseries about the rise and fall of SPIFF, a technically better format (well, according to them) that lost out to the already-becoming-ubiquitous JFIF. How many narratives in technology history are like that?

What else did I learn? Found out that if you do a sitewide search on w3.org, it'll direct you to a page powered by DuckDuckGo (instead of the more ubiquitous Google).

Quoting myself here: "a wikipedia page I don't want to be on right now, c/o fuzzy specs https://en.wikipedia.org/wiki/Pixel_density"

JFIF has two major editions, 1.01 and 1.02. The big version difference between these standards are how digital images are measured. Do you use the "dots per centimeter (or inch)" pixel density method, or do you go with pixel resolution (this many pixels by this many pixels)? There's a rich history here too, I think it'd also make for an interesting sub-sub-subsegment of codecs/standards "wars." JFIF went with the hard stance of using density, but backwards-compatible to use pixels. I guess thinking pixel density was the future, and being wrong (maybe? maybe wrong? maybe right! but I feel like we have all collectively accepted pixel x pixel sizing over "what would this be like on paper" because what even is paper? I haven't owned a printer since 2008)

This and thumbnails are the only difference between the versions.

Despite versions 1.00 barely existing and 1.01 existing for less than a year before 1.02 came out, there sure is a looooot of 1.01 JFIF files out there in the world, though.

I have/had a theory that JFIF files were frequently generated as 1.01 instead of 1.02 due to the lack of thumbnails. It's also been "not recommended" to embed thumbnails into JPEGs since the 1990s, based on the Encyclopedia of Graphics File Formats and the File Formats Handbook both discouraging it, in addition to several websites. So if you already have a 1.01 file generator, there's not that much incentive to update it to 1.02 if thumbnails aren't being added anyway. I didn't go on a deep dive to sort out if I could make a strong case for this because it doesn't really matter that much either way, but just an idea. It could also be the pixel density vs resolution thing, too -- versioning as 1.01 or 1.02 based on measuring in pixels or as density.




