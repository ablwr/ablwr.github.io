---
layout: post
title: "MediaInfoInfo: MediaInfo-specific words"
date: 2020-02-14 07:00:00 -0500
tags: [mediainfoinfo]
---

This is the seventh in a series of blog posts on a project I call "MediaInfoInfo" (with weekly associated blog posts). This project is focused on improving documentation for the ubiquitous media analysis tool [MediaInfo](https://mediaarea.net/MediaInfo).

Other posts:

1. [MediaInfoInfo: Initialize project](https://bits.ashleyblewer.com/blog/2020/01/10/mediainfoinfo-initialize-project/)
2. [MediaInfoInfo: Parameters / making a plan](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-parameters-making-a-plan/)
3. [MediaInfoInfo: General streams](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-general-streams/)
4. [MediaInfoInfo: Video streams](https://bits.ashleyblewer.com/blog/2020/01/24/mediainfoinfo-video-streams/)
5. [MediaInfoInfo: Audio streams](https://bits.ashleyblewer.com/blog/2020/01/31/mediainfoinfo-audio-streams/)
6. [MediaInfoInfo: Image, Menu, Text and Other streams](https://bits.ashleyblewer.com/blog/2020/02/07/mediainfoinfo-image-menu-text-other-streams/)
7. MediaInfoInfo: MediaInfo-specific words
8. [MediaInfoInfo: Metadata Tags](https://bits.ashleyblewer.com/blog/2020/02/21/mediainfoinfo-metadata-tags/)

# MediaInfo-specific words

Going through parameters and their definitions (or lack-thereof), I would come across certain phrases that had specific meanings in MediaInfo that are not necessarily the normal definitions in common language. Or maybe it's better to say words that are so vague/broad that it wasn't easy to make an assumption about the context here. I took note of them and had to reference them over and over again when I was working through what each parameter should mean in a clear and concise way. Here are a few of these special words. A lot of these MediaInfoInfo posts have been about my journey through the process of reviewing each section, but this post is something that I think will be especially broadly useful to people using MediaInfo now, especially in the context of deep quality control or conservation treatment work in which there are unexpected results.

## "Original"

MediaInfo makes heavy use of a parameter name, followed by `_Original`. "Original" is an ambiguous term, and to me, having an archives background, would think that it refers to the original source material (like if transcoding from one file to another type of file, and acknowledging the original in the metadata). That's not what this field is, though. MediaInfo does its best to guess, based on all the data in a file, how the file will be played back by viewers. And often, there is a battle between the container (the General stream, in MediaInfo) and the video codec (Video stream). MediaInfo guesses whether the container or the codec is likely to win this battle, but shows what the codec thinks about something in the `_Original` field. These fields are only displayed if there's a discrepency between the container and codec. It will not be present if they match. So even the presence of an "Original" indicates that there could be some wonkiness with the file when playing it back, depending on whether the codec or container "wins" the battle, according to what the player decides. If Quicktime is playing the file one way and VLC is playing it another way, this is probably the first thing to look for when running MediaInfo on the file.

## "Source"

MediaInfo uses the prefix `Source_` for a couple of different fields: `Duration`, `StreamSize`, and a few others. The parameter definitions are just the same as the standard definitions, but with "Source" in front of the rest of the definition. This took some heavy sleuthing because perusing the source code wasn't really giving me what I was looking for, but I landed on a clear explanation of the difference [on this feature request](https://sourceforge.net/p/mediainfo/feature-requests/366/#f4cf). "Source", like "Original" above, can be ambiguous. For Duration and StreamSize, it's defined as being information retrieved from the media part of the header metadata, within the track part of the header.

"Source" also appears in some newer parameters that don't yet seem to be implemented yet, like `MasteringDisplay_ColorPrimaries_Source`, but I imagine they will mean the same type of thing.

## "OriginalSource"

Because these other two were taken, `OriginalSource` is used in the General stream to describe something that details information about where the content was originally derived from, usually referencing what the content was originally recorded on, or was on prior to its digitization. These are held in metadata tags embedded in the container, rather than something coming from analysis of the media format itself. This would be that archival understanding of a definition of "Original" that I mention up above.

## "Stored"

"Stored" is a word used to distinguish where the information was derived from. Did it come from a metadata tag? Did it come from the container? Did it come from the codec? Something "Stored" is coming from what is encoded into the stream itself, rather than another part of the file that says what something should be. Instead, it is what it actually is. Again, containers and codecs can sometimes battle for what is correct, and sometimes what the container is assuming to be true is what the playback device will trust, even if that is not what is "baked in" to the stream, so-to-speak.

## "Nominal"

"Nominal" is used in two places in the MediaInfo streams -- for Bit Rate and Frame Rate. As a word, there is not really a [singular](https://en.wikipedia.org/wiki/Nominal), [clear](https://en.wikipedia.org/wiki/Real_versus_nominal_value) [definition](https://en.wiktionary.org/wiki/nominal#English) for it, so I went searching for what it could mean in this context.

I like [this definition](https://developer.apple.com/documentation/avfoundation/avassettrack/1386182-nominalframerate): "The nominal frame rate indicates the number of frames per second for tracks that carry a full frame per media sample." So for frames that are interlaced or encoded in such a way that they don't contain all of the data (and rely on neighboring frames for that data), the nominal frame rate would be different. This is the frame rate based on full frames.

For bit rate, [definitions](https://forum.videohelp.com/threads/311405-What-is-nominal-bit-rate) are a little bit different: "Nominal Bit Rate is = the max bit rate allowable by the encoding process. The bit rate does not have has to be achieved in the encoding process. It is only a max ceiling to ever allow."

But nominal is not minimum nor maximum, and these descriptions attempt to define two different meanings that I think are getting at the same concept and how it is applied to different codecs, keeping in mind that codecs can use this word in different ways, too. MediaInfo applies these couple of fields across all the different potential applicable codecs, so the definition has to be something generic.

Looking at the MediaInfo code, it is using the statistical definition of "a measurement (or group of measurements) that matches the predicted value(s) within the expected margin of error". MediaInfo is using logic like `(BitRate_Nominal>BitRate*0.95 && BitRate_Nominal<BitRate*1.05)` to determine this kind of "close-enough-ness" to see if the bit rate (or frame rate) calculations are close enough to something that is considered normal that it could and should be considered that standard rate. Like a "well, close enough" rate.

And that's it, for words that are repeated across the parameters and how they are defined. Next week, I am going to try to cover the TAGS fields and help shed some light on how those are populated, and where they come from.