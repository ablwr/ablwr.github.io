---
layout: post
title: "MediaInfoInfo: Image, Menu, Text, and Other streams"
date: 2020-02-07 06:00:00 -0500
tags: [mediainfoinfo]
---

This is the sixth in a series of blog posts on a project I call "MediaInfoInfo". This project is focused on improving documentation for the ubiquitous media analysis tool [MediaInfo](https://mediaarea.net/MediaInfo).

Previous posts:

1. [MediaInfoInfo: Initialize project](https://bits.ashleyblewer.com/blog/2020/01/10/mediainfoinfo-initialize-project/)
2. [MediaInfoInfo: Parameters / making a plan](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-parameters-making-a-plan/)
3. [MediaInfoInfo: General streams](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-general-streams/)
4. [MediaInfoInfo: Video streams](https://bits.ashleyblewer.com/blog/2020/01/24/mediainfoinfo-video-streams/)
5. [MediaInfoInfo: Audio streams](https://bits.ashleyblewer.com/blog/2020/01/31/mediainfoinfo-audio-streams/)

I've tackled the largest sections -- General, Video, and Audio. I was bracing for more weirdness when I hit these other sections, but to my surprise they were almost all completely duplicate entries from either the General or Video stream (and a few from the Audio stream), so this was not much work at all.

Image was a very close replica of Video, but smaller. There was nothing to add there that hadn't already been defined somewhere else. Menu had a new concept of `List`, along with `Chapters_Pos_Begin` and `Chapters_Pos_End`, but was otherwise relying on existing definitions from General. Other was not nearly as interesting as I thought it would be. And Text had one new parameters to define (`ElementCount`).

This gave me some time to think more about style choices and come up with a bit of a rough style guide. I had been doing that all along the way, but here I was able to cross-check each of the fields that I just wrote "repeat" on, and make sure it wasn't repeating something that would not have been applicable to other sections. Should that definition change, or are they different enough to warrant being separated? For example, if `Standard` is used in the Video stream to mean NTSC or PAL, what would it mean if it's used in the Text stream? (It's not used there.) `ColorSpace` is an example where I had set the tentative definition to be "Color profile of the video" but "video" would not necessarily be accurate for the Image stream. But is the opposite appropriate -- would "Color profile of the image" be appropriate for video?

This came up earlier when `BitDepth` was used in both Video and Audio, but they are different. Audio could not inherit that definition from Video.

What do other tools do? A lot of tools don't go through the effort of defining their dictionaries. Exiftool will list out all of the potential tags, of which there are a lot, and I suppose you could read each specification to know more. FFprobe does a good job of handling a lot of data fields in a clean way, and indicates what data type the field results will be in (like int, boolean, string, etc), a quick definition, and what the default value is, if any.

In addition to keeping the definitions repeatable and openly applicable, here are some things I had been keeping in mind:

- Keeping things consistent: use of periods or not, when to use a comma and when to use parentheses, etc.
- The MediaInfo --Help page follows the same style as I have been following -- don't end a definition with a period, unless breaking into two full sentences, which I try to avoid but sometimes has to happen. This seems to be what other tools do.
- There's conflicting use of "color" and "colour" in the names and their definitions. But "color" is used consistently in the public-facing language, which seems to default to using American English. This is kind of a problem in the video space more broadly, especially with a lot of standards coming out of the US-focused SMPTE organization.

So this post is not as big as I thought it would be, because there ended up being not as much to do other than review what has already been written, which I am sort of in a constant state of doing. I have at least two more blog posts planned, so stay tuned!

