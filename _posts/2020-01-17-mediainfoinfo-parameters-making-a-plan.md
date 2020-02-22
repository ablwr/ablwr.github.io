---
layout: post
title: "MediaInfoInfo: Parameters and making a plan"
date: 2020-01-17 02:00:00 -0500
tags: [mediainfoinfo]
---

This is the second of what will be a series of blog posts on a project I call "MediaInfoInfo". This project is focused on improving documentation for the ubiquitous media analysis tool [MediaInfo](https://mediaarea.net/MediaInfo).

Following up on the [initial post](https://bits.ashleyblewer.com/blog/2020/01/10/mediainfoinfo-initialize-project/), it's time to dig into what some of these parameters are and how they are set up. This post is still a bit more "meta" and talking about taking on the project itself, but don't worry -- the next post will be getting into the details of the General stream (aka the container/wrapper).

Other posts:

1. [MediaInfoInfo: Initialize project](https://bits.ashleyblewer.com/blog/2020/01/10/mediainfoinfo-initialize-project/)
2. MediaInfoInfo: Parameters / making a plan
3. [MediaInfoInfo: General streams](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-general-streams/)
4. [MediaInfoInfo: Video streams](https://bits.ashleyblewer.com/blog/2020/01/24/mediainfoinfo-video-streams/)
5. [MediaInfoInfo: Audio streams](https://bits.ashleyblewer.com/blog/2020/01/31/mediainfoinfo-audio-streams/)
6. [MediaInfoInfo: Image, Menu, Text and Other streams](https://bits.ashleyblewer.com/blog/2020/02/07/mediainfoinfo-image-menu-text-other-streams/)
7. [MediaInfoInfo: MediaInfo-specific words](https://bits.ashleyblewer.com/blog/2020/02/14/mediainfoinfo-mediainfo-specific-words/)
8. [MediaInfoInfo: Metadata Tags](https://bits.ashleyblewer.com/blog/2020/02/21/mediainfoinfo-metadata-tags/)

The MediaInfo parameters are essentially divided up like so:

- Audio -- 280 lines
- General -- 331 lines
- Image -- 124 lines
- Menu -- 94 lines
- Other -- 188 lines
- Text -- 238 lines
- Video -- 377 lines

In total: **1632 definitions**.

Many of these definitions are "repeats", in a way. They are the same data but populated as a different output. The best way, to me, is to utilize this separation to break the work into smaller pieces and make those 1632 definitions less daunting, and then come back around to each to make sure the language I'm using is consistent. I'll start with General, and then move to Video, which is the biggest of the bunch. Then, I'll move to Audio, and follow up with Image. Then, I'll tackle Text. And Other. And then, finally, Menu. This seems to be the order of significance, based on my experience.

First, I had to get these CSVs into shape so it would be easy for me to compare the current value with my new, proposed value. I didn't want to just overwrite and use `git diff` to compare the results -- I wanted to be able to read them side-by-side and take notes. For that, I imported each of the CSVs into a spreadsheet processor, which fortunately was able to understand that they are semicolon-delimited and not comma-delimited when I asked it nicely. I made a column for the parameter, a column for the current definition, a column for my proposed definition, and a column for notes while I sorted each of them out. (They live [here](https://drive.google.com/drive/folders/1hPClSWIyqmCibs7cQzKIri6ILKo2-oNS?usp=sharing) while I work on them, by the way!)

I figured out the syntax and what each of the columns represent when I worked on this 6 months ago, but I've since forgotten. I learned enough to learn that it didn't really matter to me, because I was only changing the definition value, and it was obvious where that is. The others indicate whether a field is the default, or should only be shown when using the `-f` mode for "Full", and stuff like that.

The first letter is always Y or N. Y for Yes, include in the output. N for No, don't include in the standard output.

The next string of letters are one of the following: NI, NT, YI, NTY, YTY, NIY, YFY, NFN, YNY. In this string, it seems that an I signified Integer, T signifies Text, and F signifies Float. I think the N or Ys indicate if showing nothing is acceptable, and whether to show the field if the result is nothing. I'm not totally sure about that, and am waiting to get a [direct answer about it](https://github.com/MediaArea/MediaInfoLib/pull/1207#issuecomment-574878381). It's not something that stops me from working -- and there is a lot of work to do.

Some rows in General have six semicolons, and others have eight, but the definition is still the seventh entry (out of 7, or 9). I think this is when the General track gets more specific and represents aspects of tag metadata, chapters or the menu field (but there is a Menu.csv to parse, too). I'll get to that when I get to that.

A big thing is how many fields repeat between each of the sections. For now, I am thinking about them in a way that has me thinking through the best definition in General.csv -- which will make the first group I work on take the longest amount of time, and then copy those definitions into the others when they are mostly finalized. The definitions are general enough to be applicable for all of the streams.

Things I am thinking about right now is the concept of a style guide -- what kind of patterns will I create and have to stick with, and will have to work for every definition? I need to research what other kinds of tools do. And the other thing I am thinking about is where to pull information from. Here are the source I've been working with:

**Source code**
Obviously I start here first, which gives me an idea of how often a definition is used, which section it is used for, and if there are any specific values associated (for example, some parameter values are always going to only be Yes or No).

**History.txt**
The changelog for the project has helped me understand when certain fields came into existence (or became deprecated), and sometimes there are definitions in the History logs when the current parameters definition is very slim.

**Official discussion forum**
MediaInfo has lived for a very long time on SourceForge, where there is a [discussion forum](https://sourceforge.net/p/mediainfo/discussion) and full history available. It is a rich history, and I have figured out a lot of vague definitions by looking here.

**Bug tracker**
If the discussion forum has nothing to offer, some things have been explained in the past on the SourceForge [bug tracker](https://sourceforge.net/p/mediainfo/bugs/), or the current [GitHub Issues page](https://github.com/MediaArea/MediaInfoLib/issues).

**Doom9 Forums**
If these fail, there is a popular forum for digital video called [Doom9](http://forum.doom9.org/), and a lot of people have asked in-depth technical questions about MediaInfo here, over the years.

**The general internet**
There are lots of online web forums where people are discussing the results from MediaInfo and how they are confused about their messed up files, not just the one I named above. Online forums are such a wonderful part of the open web, and it makes me bummed that so much of these conversations have been locked up into Facebook groups or other walled gardens, and won't leave such a rich history as these other open, independent forums running on open source software.

Okay, I didn't mean to get all philosophical there, at the end, but I did anyway. This is my plan of action for the next few weeks, as I try to quickly tackle all of the parameters (spoiler alert: General is already in the "draft review" phase) and finalize a large pull request for review. I am eager to get a head-start on this, since I have a full-time job, a mini part-time job, and I teach a graduate class, but I don't want to get behind on this "winter break" project after my graduate class starts in only a little bit more than a week!