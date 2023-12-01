---
layout: post
title: "Researching file formats 14: Apple EMLX Format"
date: 2023-12-01 07:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

In typical Apple fashion, this is a variation of an open and well-adopted standard (the [EML format](https://www.loc.gov/preservation/digital/formats/fdd/fdd000388.shtml)), modified slightly just to be Apple-specific, and [totally undocumented](https://stackoverflow.com/questions/884440/documentation-on-apple-mails-emlx-data-structures-for-conversion-purposes).

Got a kick out of this update to a blog post from [jwz](https://www.jwz.org/blog/2005/07/emlx-flags/) that reads "**Update:** Please, people, I asked a very straightfoward question. I'm not interested in your _guesses_. I can guess too. I'm looking for _facts_. I can also reverse-engineer at least some of it, if I have to. But I'd rather not, if it's actually documented somewhere. Which is why I asked. If you don't know, put your hand down." 
...because yes, I feel that sentiment very deeply while working on these formats. No opinions, facts only! PLEASE!

Found this [life advice](https://mailboxreader.wordpress.com/2017/03/17/view-mac-emlx-files-in-windows/)(???) while researching: "Life has become a race. Everyone is in search of something better than the best. In such a scenario, it is important for users to work without any barrier. Therefore, in this write-up how to Open & Read EMLX Files with every other platform using different methods has been described in details."

Anyway, EMLX stores a single message for Apple Mail (the default mail application in macOS) and they are typically found around `~/Library/Mail/Mailboxes/` inside of an MBOX folder. Converting them to a standard MBOX format seems not-too-hard, based on the ways to deal with these being scripts that are only a couple-hundred lines (like [this one in Ruby](https://github.com/imdatsolak/elmx2mbox), for example, but there are others).

I don't have much more to say about this format. To counter the proprietary-format stuff, I do have appreciation for jwz's 18 years of technical blogging, and that the content was successfully migrated off of the livejournal platform at some point, and onto his own domain before it was lost to time / a sale / etc. It still has the exact aesthetic of livejournal, so I'm assuming its the same code (hello, Perl), since the livejournal software was open source (at least until 2014!).

I just read a YA novel that included some livejournal entries. Does that make it a period piece??? It's set in 2006. It was [Girls like Girls](https://bookshop.org/p/books/untitled-secaa-anonymous-secaa/18721509?ean=9781250817631) by Hayley Kiyoko, for anyone else interested in that era.