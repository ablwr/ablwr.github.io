---
layout: post
title: "Researching file formats 12: Kryoflux raw disk image format"
date: 2023-11-17 09:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [KryoFlux Stream File](https://www.loc.gov/preservation/digital/formats/fdd/fdd000610.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

One of the things I know about Kryoflux is it has a bad reputation in multiple ways. [ArchiveTeam](https://wiki.archiveteam.org/index.php/Rescuing_Floppy_Disks#Kryoflux) has a strongly-worded blurb about concerns over the licensing agreement.

Working on this format had me thinking a lot about the problem with companies that are closed-off or have really sketchy business practices, especially when the company does a lot of fear-mongering among members of the community, but only in ways that are elusive.

For example, I've been personally bullied/threatened by the folks at (redacted), the digital preservation software platform, but I'm just one anecdotal example who has been told about another handful of anecdotal examples of this happening to others, too. But in terms of actually coming up with what a company is like, in a way that you can actually and formally point to, is near-impossible because companies or people who are like that tend to intentionally perform actions in a way where they know they won't be caught or leave a trace.

This whole format thus took me down a dark path, really dwelling on how hard it is to know these things, and even harder to be able to try to warn others. (Including meta-paths about this very blog post, whether I redact the above name or not, the dangers that plays in my career, etc.) I could come up with another handful of additional people who have done much worse things to me over the course of my career than the above example, and I've been deeply hurt just by circumstance of being in the wrong place at the wrong time, and being damaged by the arbitrary whims and power struggles of other people that shouldn't even have involved me in the first place. I struggle so much trying to deal with these fallout of these things on a daily basis, personally, and I've lost _sooooo many_ hours of my life just feeling stuck because of it.

The whole disk imaging community has a lot of its own drama going on, so it's been a lot to wade through in order to do my job and create something that is impartial. It puts me off of the whole thing, and this set was a real struggle to work through.

Anyway, back to Kryoflux, I really only care about the format (in this context, for this project) and not the politics around the disk imaging community, although getting to the bottom of the rumor that some files created are allegedly all owned by Kryoflux, or have a viral free license, or whatever else is something that matters in terms of whether it's a file suitable for digital preservation.

There is a lot of general writing on this system, including dedicated works [by archivists](https://github.com/archivistsguidetokryoflux/archivists-guide-to-kryoflux/tree/master) and lots of hobbyist forum posts. Despite the politics-by-which-I-must-tread-lightly, the format itself is intended to be fairly light, a light metadata-infused wrapper that holds the raw transferred data.

On a lighter note, I kept having to download PDFs to read about this format, which annoyed me when it came to cite-source-to-pass-to-colleague time.
