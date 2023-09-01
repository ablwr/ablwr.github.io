---
layout: post
title: "Researching file formats 4: Exif (Exchangable Image File Format)"
date: 2023-09-01 09:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Hot on the tails of the JFIF format family, time to crack into the Exif family. (That's short for "Exchangable image file format")

Like JFIF, LC [already has an entry for EXIF](https://www.loc.gov/preservation/digital/formats/fdd/fdd000146.shtml) so that makes for a good starting point.

["Everything you wanted to know about media metadata, but were afraid to ask"](https://freedom.press/training/everything-you-wanted-know-about-media-metadata-were-afraid-ask/) is a nice post for beginners about interpreting exif data using exiftool.

This is an interesting format because it's a format that is made up of other formats. That makes it both easy to work on and more difficult at the same time. I also think it's funny how it's fundamentally an image format but then they're like "ehhhhh lets throw audio in there too though!" I think it's a good example of a format having to grow to fit one major use case (digital cameras) as the use case continued to grow (cameras that can take/create small video clips with sound). Exif files have also grown beyond digital cameras and are used for printers, scanners, phones that are "smart", etc. And then Exif metadata has expanded as well, to be used more of a metadata standard rather than a file format standard, with people popping Exif data into all sorts of files, whether they are traditionally "Exif" files or not. So there was this one idea that came into the world, became a real structure, and then the world continued to grow around it and it had to adapt and adjust accordingly, in official and unofficial ways. I think that's beautiful even if it's also annoying for me.

I feel like I have more of a series of jumbled thoughts for this one. Here's some small notes that could all grow out into their own blog posts (and maybe they will, as I move through the review and editing process):

- Learned a new word: [Hot shoe](https://en.wikipedia.org/wiki/Hot_shoe) (the lil metal mounting pad on top of a camera)
* Q's from the spec: "Box format" in APP11? Oh it's just for JPEG
* If metadata is removed from an Exif file, is it still an Exif file or is it just a JPEG/TIFF/WAV? (for the reader to consider)
* FlashPix (no comment)
* MakerNote tag and issues there
