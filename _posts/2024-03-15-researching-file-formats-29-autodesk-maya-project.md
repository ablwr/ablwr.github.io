---
layout: post
title: "Researching file formats 29: Autodesk Maya Project"
date: 2024-03-15 09:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [Maya ASCII Scene File Format](https://www.loc.gov/preservation/digital/formats/fdd/fdd000604.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

This format described 3D scenes -- geometry, lighting, animation, rendering, other stuff. It's fairly straightforward, and I felt the [documentation](https://download.autodesk.com/us/maya/2010help/index.html?url=Maya_ASCII_file_format_Organization_of_Maya_ASCII_files.htm,topicNumber=d0e678001) was relatively thorough while being succinct.

Preservation issues seem to mostly be around concerns with this file needing to be connected to other files:

Here's what the specification has to say about this format: "If you want to write a program to translate Maya ASCII files to other file formats, you have a difficult job ahead of you. To do the job properly, you would not only need to be able to read in the files, but also to read in the referenced files. Since MEL references can contain any arbitrary MEL code, you would either have to not support them, or write a full MEL interpreter."

(MEL is the Autodesk Maya scripting language)

This format really digs into the intricacies that I feel like the folks at the [Software Preservation Network](https://www.softwarepreservationnetwork.org/) are tackling, and something [Rhizome](https://rhizome.org/) has been thinking about for a very long time, around files that [depend upon](https://en.wikipedia.org/wiki/The_Red_Wheelbarrow) other files. 