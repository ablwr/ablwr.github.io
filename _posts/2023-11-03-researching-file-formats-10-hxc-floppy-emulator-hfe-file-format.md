---
layout: post
title: "Researching file formats 10: HxC Floppy Emulator HFE File Format"
date: 2023-11-03 07:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

My starting point for this format was [this PDF](https://hxc2001.com/download/floppy_drive_emulator/SDCard_HxC_Floppy_Emulator_HFE_file_format.pdf) (with a sweet logo). And I spent a lot of time [deep in the forums](https://stardot.org.uk/forums/viewtopic.php?p=279138&sid=33f74a30d3a0dfb1c2581a3129a99f80#p279138) on this one.

It was nice to see a forum (and associated discords) be so active on the topic of floppy disk emulation -- I had no idea, the reach. Maybe because it's relatively simple and accessible to get into? Maybe because people really love games? I don't know.

So, this format. This format has a 1.5-page PDF as a specification, which a lot of people question as being thorough enough to be a real format. It is pretty slim, yeah.

There's also the question of versions: The decades-old PDF on the website is a version 1.1. There's an unlisted version 1.0, allegedly a version 2, and there's a more-commonly-used version 3 that is only documented in the source code (and that's cannon -- from the format author). Oh, and there's a HFE stream format, too. So that was the big challenge with this format, a lack of clarity and the profound unhelpfulness at being told to "just look at the source code", which, in my expert opinion, doesn't have the answers that a well-written specification document would provide (especially when neither the source specification _nor_ code is very clear).

Yeah, perhaps a short entry here -- I don't have too much to say on this one except if you want to know more, you'll just have to read the source. ;)

The next two posts will also be about floppy emulation formats, stay tuned for MOOF and Kryoflux! But don't get too excited, because I will still be grumpy about the whole format set.
