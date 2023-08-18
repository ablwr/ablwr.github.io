---
layout: post
title: "Researching file formats 2: MySQL Table Definition Format"
date: 2023-08-11 08:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

This format took me on an interesting journey deep into the debts of MySQL. Not just any MySQL, but legacy, nearly-deprecated, "during or before shit hit the fan" MySQL.

I laughed out loud when I came across this summary of the format:

> "Table definitions are in FRM files on disk, entirely managed by MySQL (not the storage engines) and **for your own sanity you should not ever look into the actual file format.**"

From [this 2014 blog post from a former MySQL developer](
https://www.flamingspork.com/blog/2014/09/19/mysql-architecture/)
(Emphasis mine)
(And it's a great read, the entire series, so check it out!)

If you're a video-watcher instead of a blog-reader, here's a gem of a talk from the same person: [Past, Present and Future of MySQL and variants](https://www.youtube.com/watch?v=6Uv9vcb4SdA&t=4s)

Here's another fun quote I came across:
["Let it not be said that the .frm file format is forgotten!!" ](https://dba.stackexchange.com/questions/208198/mysql-frm-file-format-how-to-extract-column-info/215330#215330)-- bcperth, Aug 19, 2018

MySQL has no limit to the amount of tables you can add. What can I do with that information? >:) JK, I ran across a few blog posts that went into the realistic limits. Unfortunately I didn't save them because it wasn't applicable to writing a summary of this format, but they are out there. And anyway, the answer is "it depends."

I've spent a lot of time thinking about open source licensing and formats and software and governance and MySQL is not fun to look into.

Last format had me thinking about the generally-accepted use of a format and how it differs from the legacy specification. This format had me thinking:
*How do you explain that the legacy documentation is wrong?*

A lot of the blog posts from MySQL developers, or StackOverflow posts, or old forum posts, would complain about how MySQL's docs were just incorrect. The docs for this format were deleted off the web, even though the legacy version is still up, and is available [on the wayback machine](https://web.archive.org/web/20221007195420/http://dev.mysql.com/doc/internals/en/frm-file-format.html), and are also just a bit weird because they include some opinions instead of, y'know, a specification to work off of. So this format required a bit more basic reverse engineering than others because there weren't real facts to go off of.

This format took me on the "do not cross down this path!" warning journey, but it also was conflated with another format. Turns out MySQL (and MariaDB) also will excrete a .frm file if you ask it to create a new view (at least in older versions). It creates a file that is either binary or text, and it puts it in the same place, but it's like, a completely different type of file from the Table Definition Format file (which is always binary, and stores table definitions). This other, *imposter???* .frm stores just the query to get a specific view, key/value pairs for the defined query and some other metadata, and doesn't have anything to do with these other .frm files that can be used to back up the entire MySQL database. We concluded it should be its own format ("MySQL View Definition Format"), so it will be. (But I will not make a dedicated blog post for it).

I don't know why LC chose this format and not the two pair formats, MYD and MYI, which can be used to help restore a lost legacy database, but know that you'll need all three if you want to. And this format, the .frm, doesn't even store that much, just the table definitions. They're important, but less important than the _data_!

And on that note, that's it for two "database" formats. The next couple of posts will be on image format families!