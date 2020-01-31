---
layout: post
title: "MediaInfoInfo: Audio streams"
date: 2020-01-31 06:00:00 -0500
tags: [mediainfoinfo]
---

This is the fifth!! in a series of blog posts on a project I call "MediaInfoInfo" (with weekly associated blog posts). This project is focused on improving documentation for the ubiquitous media analysis tool [MediaInfo](https://mediaarea.net/MediaInfo).

Previous posts:

1. [MediaInfoInfo: Initialize project](https://bits.ashleyblewer.com/blog/2020/01/10/mediainfoinfo-initialize-project/)
2. [MediaInfoInfo: Parameters / making a plan](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-parameters-making-a-plan/)
3. [MediaInfoInfo: General streams](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-general-streams/)
4. [MediaInfoInfo: Video streams](https://bits.ashleyblewer.com/blog/2020/01/24/mediainfoinfo-video-streams/)

# Audio!

Like the Video streams section, the Audio section has specific format settings that are identified and described by MediaInfo. This involved me reading some MPEG Audio and Vorbis specs to determine what some of the Format Settings mean, because they had no definitions, and reading through wikipedia pages on Dolby Digital and ambisonics. My lack of knowledge is kind of embarrassing, especially considering the number of years I spent working at a record store having to listen to people talk about their equipment and working in college radio, where I had to have had some basic level of audio editing. But I've never been one of those hi-fi bros, so I guess it all washed over me. Not gonna lie -- this section was the hardest, due to my relative lack of knowledge about audio format settings, compared to video. From reading the code and looking through past issues or discussions, it was harder to tell what the expected output of some of these parameters are, and a few seemed to not be in use, so it was harder to get details or examples.


## Album_ReplayGain_Gain

One of the things that stumped me when going through the General field was the parameter `Album_ReplayGain_Gain`. What a mouthful, right? It's an ID3v2 tag and led me on a bit of an unexpected journey. I was trying to make sure I understood what this was all about, and stumbled upon [this forum](https://hydrogenaud.io/index.php?topic=52991.0), which led me to this [website](https://www.digido.com/news-digital-domain/?file=article&sid=9), referencing an [article about audiophiles and how much money they pay for equipment](https://www.digido.com/wp-content/uploads/2017/04/Sex-With-A-Proper-Stereo-small.pdf). The other link involved mostly [math equations](https://en.wikipedia.org/wiki/Sound_pressure#Sound_pressure_level), so I went with the Village Voice article from 1981. Which weirdly I feel like I have read before, but it could be that there are a lot of articles like this out there. But it was funny that one of the articles for video equipment was for this mysterious store called "Uncle Steve, Inc", and the address is for [one of my favorite buildings in NYC](https://www.google.com/maps/place/343+Canal+St,+New+York,+NY+10013/@40.7206185,-74.0036007,3a,75y,39.58h,95.93t/data=!3m7!1e1!3m5!1sMIDzGz-3hzDEgyaUYFx7UA!2e0!6s%2F%2Fgeo2.ggpht.com%2Fcbk%3Fpanoid%3DMIDzGz-3hzDEgyaUYFx7UA%26output%3Dthumbnail%26cb_client%3Dsearch.gws-prod.gps%26thumb%3D2%26w%3D86%26h%3D86%26yaw%3D48.485405%26pitch%3D0%26thumbfov%3D100!7i16384!8i8192!4m5!3m4!1s0x89c2598a54f94c6d:0xf3bc8f5632d661d6!8m2!3d40.7208025!4d-74.0033703)! I used to pass it weekly. I like how it feels like it's really hanging in there, while this neighborhood transforms into extremely high-end apartment buildings. Anyway, the article is fun, too.

Anyway, sorry, I went the "~digital humanities~" route instead of coming up with the perfect research at hand -- information about replay gain. The present definition was fine, so things are fine.


## Default and Forced flags

In MediaInfo, the definitions for Default and Forced are the same (soon-to-be "were the same"). They are similar, but not quite the same, as outlined when this issue came up and the feature request was put in [here](https://sourceforge.net/p/mediainfo/discussion/297610/thread/0710d178/) and answered well [here](https://gitlab.com/mbunkus/mkvtoolnix/-/wikis/Default-and-forced-flags-and-default-yes-no-in-the-GUI) (for another great open source tool, [mkvtoolnix](https://mkvtoolnix.download/). I first came across it in the Video stream section, although this seems to be much more common for the Audio or Text streams, and is especially useful for handling subtitles. 


## Channel positions

Channel positions seem to just be difficult to define and succinctly describe, in general. MediaInfo takes this information directly from the specification, when working on how to describe the layout of something like surround sound. It can end up looking mostly-readable like `Front: L C R, Side: L R, Back: L R, LFE`, or get condensed into something like `L R C LFE Ls Rs Lb Rb`. There's also the option to receive these positions as `x/y.z` format, which is like `3/2/0.1` for something that may be advertised as "5.1 Dolby Digital Surround Sound".

## Other things

Just like in the previous blog post, here are a few things I read up on in order to secure the proper definitions:

- [Spectral band replication](https://en.wikipedia.org/wiki/Spectral_band_replication)
- [Parametric stereo](https://en.wikipedia.org/wiki/Parametric_Stereo)
- [Vorbis spectral floor](https://xiph.org/vorbis/doc/Vorbis_I_spec.html#x1-150001.2.4)
- [MPEG Audio frame header information](http://mpgedit.org/mpgedit/mpeg_format/mpeghdr.htm)

Also, [here](http://forum.doom9.org/archive/index.php/t-93469.html)'s a good forum post on interleaving and how that works within frames.

That's all I have for now, until next time! I'll be covering the last handful of sections: Image, Menu, Text, and Other.