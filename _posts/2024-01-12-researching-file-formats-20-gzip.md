---
layout: post
title: "Researching file formats 20: gzip"
date: 2024-01-12 09:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [GZIP](https://www.loc.gov/preservation/digital/formats/fdd/fdd000599.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

Am I running out of steam or is there not that much to say about gzip? I think the biggest struggle in writing about the sustainability of this format is ensuring there isn't conflation between the format itself (compression algorithm, in this case) and the software tool of the same name that creates this format. They are tightly linked together, but different, so I had to make my research notes explicit in every case so it's easier for when I turn it over to the writer/editor on this project.

A gzip file contains:
- a 10-byte header. This header contains its magic number ("1F8B08"), a version number and a time stamp,
- optional extra headers, such as the original file name,
- a body, containing a DEFLATE-compressed payload,
- and an 8-byte footer, containing a CRC-32 checksum and the length of the original uncompressed data.


I did come across this [very thorough StackOverflow answer](https://stackoverflow.com/questions/20762094/how-are-zlib-gzip-and-zip-related-what-do-they-have-in-common-and-how-are-they/20765054#20765054) about gzip (and its relation/difference to other formats of similar names), and the comments are funny, because someone is like "It'd be great if this had cited sources" and the answer, which was written by one of the original authors of gzip, was "I am the reference, having been part of all of that."

