---
layout: post
title: "Researching file formats 30: Autodesk Maya Binary"
date: 2024-03-22 08:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

You know, I saved a spot for this format but it really is essentially the same as [last week](https://bits.ashleyblewer.com/blog/2024/03/15/researching-file-formats-29-autodesk-maya-project/)'s, except stored in a binary format instead of a text-based one. I checked to see if it was simply gzipped, but it wasn't -- it's its own secret-sauce thing courtesy of Autodesk (as usual, comments welcome, maybe it is something obvious, but since these format documents are about _solid citable proof_, these paths of investigation are fun but not directly useful to the task at hand, if that makes sense).

Most users seem to come to the conclusion that saving work as MA is better, because there's a better change you'll be able to see, understand, and fix something later, whereas the binary files are totally opaque. On the other hand, there's compression happening and the files are smaller as a result, and also load into systems faster. So I suppose it can depend on if the files are meant to be actively worked on heavily, or meant more for storage and later processing.

I've dealt with closely related files a few times for this project, and there's no clear cut way to know if formats should be described together or split into two different formats. In a couple of weeks, I'll have a post about Apple ProRAW files, which ended up being broken into two formats instead of just one. These two could possibly have been consolidated into one, but they will remain as two.

Something that came up a couple times during this project, and during these two sibling Autodesk Maya formats, is that companies have started to shift towards the cloud model, resulting in the lack of file formats entirely, and especially the lack of any external documentation or support, hence this format having documentation from 2010 and 2011, but not future versions (even though the format is still being used and is the default export format). Something to think on!