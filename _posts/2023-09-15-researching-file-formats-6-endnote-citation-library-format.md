---
layout: post
title: "Researching file formats 6: EndNote Citation Library Format"
date: 2023-09-15 09:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

**Meta-note: This blog series aims to run once a week, but there won't be posts for the next THREE weeks, as I'll be on vacation and offline. Series to resume Oct. 13th.**

Big thanks to [Tyler Thorsted](https://preservation.tylerthorsted.com/) for providing me with _many_ sample files for this format (and for doing research that led to some [thorough PRONOM entries](https://www.nationalarchives.gov.uk/PRONOM/fmt/325)).

EndNote! Not to be confused with [Evernote](https://arstechnica.com/gadgets/2023/07/evernote-the-memory-app-people-forgot-about-lays-off-entire-us-staff/), who has recently met its demise. 

Whatever I knew about reference and citation management, I forgot immediately upon graduating college. Endnote calls itself the "best reference management tool", which is a pretty bold claim and probably totally fucking false.

I got riled up reading [the Wikipedia page on EndNote](https://en.wikipedia.org/wiki/EndNote) where it mentions that the owners sued Virginia, *the ~~state~~ Commonwealth*, over Zotero being able to import EndNote databases. My god!!! Go to hell, EndNote (or the owners at the time, which was a Canadian company that sounds like a person's name, and there's even MORE weird drama around this too)! Read more on Wikipedia and beyond, I'm not gonna go into it here. Sounds dramatic. File formats are so dramatic.

- [Court order](https://web.archive.org/web/20090124084642/https://www.courthousenews.com/2008/09/17/ReutersvVirginia.pdf)
- [an article about it]([https://libraries.mit.edu/news/endnote-zotero/1207/](https://libraries.mit.edu/news/endnote-zotero/1207/))
- [another article about it](https://arstechnica.com/information-technology/2009/06/thomson-reuters-suit-against-zotero-software-dismissed/)

Okay one more thing, EndNote's current owning company, Clarivate's American HQ is/was (???) right here in Philadelphia where they have some [mixed reviews](https://www.glassdoor.com/Reviews/Clarivate-Philadelphia-Reviews-EI_IE1556432.0,9_IL.10,22_IM676.htm?filter.iso3Language=eng).

Also the Clarivate website (including subdomains) kept timing out for me, which is ridiculous because they are like a billion-dollar company??? The bar is so low for enterprise.

ONTO THE FORMAT (see, this is the kind of thing that can't end up in the actual end product):

The format itself, like the [MySQL table definition format](https://bits.ashleyblewer.com/blog/2023/08/11/researching-file-formats-2-mysql-table-definition-format/), works well when paired with some of its siblings, because it can be used to back up and restore a collection.

This format is bonkers though, like I thought the MySQL Table Definition Format and View Definition Format were a little wacky because MySQL was also generating totally different files with the same extension, but EndNote keeps the file extension (if its used at all) and format while totally changing its contents, shaping it all sorts of different ways.

The [PRONOM definition for one of the format types](https://www.nationalarchives.gov.uk/PRONOM/fmt/325) sums this up well. And the [ArchiveTeam File Format Wiki](http://fileformats.archiveteam.org/wiki/EndNote_Library) sums it up even more succinctly.

Also, first, the versioning!!! 1 ... 9, X ... X9, 20. WHYYY. The first block of versions use a binary file, then the second wave uses a zip file, and then they switch it to SQL Lite, and compression was added in there at some point for some formats, and a lot of versions just don't even try to be backwards compatible. AND sometimes the software will just auto-convert the version for you. What a mess!

- Versions 1 - 9: Binary file type
- Versions X to X9: ZIP container format
- Version 20: ZIP compressed SQLite database type of format. 


I still can't not get riled up about how this is horrible software and they had the audacity to sue a ~~state~~ Commonwealth over a different but open source type of software!!!

For real professional thoughts on this format, you'll have to wait for the new record to be published. :)











