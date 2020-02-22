---
layout: post
title: "MediaInfoInfo: Metadata tags"
date: 2020-02-21 09:00:00 -0500
tags: [mediainfoinfo]
---

This is the eight and (perhaps) penultimate in a series of blog posts on a project I call "MediaInfoInfo". (And the last until this project is able to be wrapped up after code review, which hasn't started yet so it could be a while.) Anyway, I suppose this means that this is the last of the weekly post series. This project is focused on improving documentation for the ubiquitous media analysis tool [MediaInfo](https://mediaarea.net/MediaInfo). 

1. [MediaInfoInfo: Initialize project](https://bits.ashleyblewer.com/blog/2020/01/10/mediainfoinfo-initialize-project/)
2. [MediaInfoInfo: Parameters / making a plan](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-parameters-making-a-plan/)
3. [MediaInfoInfo: General streams](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-general-streams/)
4. [MediaInfoInfo: Video streams](https://bits.ashleyblewer.com/blog/2020/01/24/mediainfoinfo-video-streams/)
5. [MediaInfoInfo: Audio streams](https://bits.ashleyblewer.com/blog/2020/01/31/mediainfoinfo-audio-streams/)
6. [MediaInfoInfo: Image, Menu, Text and Other streams](https://bits.ashleyblewer.com/blog/2020/02/07/mediainfoinfo-image-menu-text-other-streams/)
7. [MediaInfoInfo: MediaInfo-specific words](https://bits.ashleyblewer.com/blog/2020/02/14/mediainfoinfo-mediainfo-specific-words/)

# Tags

Something I started looking into but determined I'd come back to later are the tags sections. Mostly, I wanted to know if it was worth it to get granular enough into defining where the tags are coming from, and if they are part of a certain standard or were derived from a certain specification. Fundamentally, I think that many do, but some are a mix of whichever are available, so I determined that they could not each have their own definitions citing their "provenance." Plus I don't know how these will continue to be defined in the future, with new formats or further analysis into each of the tags. But I learned where each of the parsings take place, and how they are mapped from the embedded metadata codes into something presented to the end user. Below is an example of a few of those. That's not to say that metadata doesn't get collected, parsed, and written all over the place, but sometimes it was in little bundles that are easy to read if you're willing to get your hands dirty and dig into the codebase a little bit.

This isn't always a direct mapping, because the variable definitions end up getting mapping again to this [long list of default language fields](https://github.com/MediaArea/MediaInfoLib/blob/master/Source/Resource/Text/Language/DefaultLanguage.csv). You'll have to make the connection between the original piece of code, the variable it gets mapped to, and this list for a perfect mapping, but just replacing the underscores in "General_DistributedBy" to be "General" and "Distributed by" should be roughly enough. You would only need that second part if you need it to be perfect-perfect like for a code-parsing thing, and even still there's probably a better way to do that.

Here's a roundup of some of the tags and where in the code they get mapped to the words that MediaInfo displays, and what term is used when that happens (or if it doesn't happen -- some get passed over). 

## ID3v2 tags

Many metadata roads lead to [ID3 tag version 2.x](http://id3.org/Home). [This](http://id3.org/id3v2.3.0) is not the latest version, but it's the easest to read. This format was intended for MP3s but it has extended into and influenced other tagging systems that hold metadata embedded inside of other kinds of files in different ways.

MediaInfo does some interesting things with the ID3v2 mappings, and you can see how things work [here](https://github.com/MediaArea/MediaInfoLib/blob/master/Source/MediaInfo/Tag/File_Id3v2.cpp#L1167-L1407).


## Quicktime tags

Like ID3v2 moving beyond MP3, Quicktime tags seem to extend beyond just its original Quicktime File Format (QTFF) scope. [Here](https://github.com/MediaArea/MediaInfoLib/blob/master/Source/MediaInfo/Multiple/File_Mpeg4.cpp#L2799-L2889) is where embedded information stored in the `moov` atom, like from iTunes metadata, is identified and extracted from the [4CC data](http://fourcc.org/fourcc.php).

## Broadcast Wave Format metadata

[Here](https://github.com/MediaArea/MediaInfoLib/blob/master/Source/MediaInfo/Multiple/File_Riff_Elements.cpp#L2322-L2373) is where MediaInfo takes all the header data that makes BWF files become extra-special WAV files and transforms them into human-readable parameters. 


## Matroska tags

[Here](https://github.com/MediaArea/MediaInfoLib/blob/master/Source/MediaInfo/Multiple/File_Mk.cpp#L3141-L3186) is where Matroska tags are mapped into MediaInfo elements. This is not an exclusive list of possible Matroska tags, but the ones deemed worth pulling out and presenting.

## Vorbis tags

[Here](https://github.com/MediaArea/MediaInfoLib/blob/master/Source/MediaInfo/Tag/File_VorbisCom.cpp#L215-L354) are a bunch of tags that fit into the Vorbis Comments metadata container. This also applies to Theora, Opus, FLAC, and some other file formats. Vorbis tags seems a bit tricky because they can be any `FieldName=Data` format, so it just has to be common enough to be added here, like specific pieces of software that allow for the adding of this metadata (Hello, MusicBrainz).

## Flash Video tags

[Here](https://github.com/MediaArea/MediaInfoLib/blob/master/Source/MediaInfo/Multiple/File_Flv.cpp#L1585-L1608) are a few sparse places where metadata tags are grabbed from the source and mapped into output fields. Flash isn't an open specification so this could be useful to people that have to work with recovering these little files.


## Other resources

Outside of MediaInfo, the Matroska folks have made a [metadata mapping spreadsheet](https://www.matroska.org/technical/specs/tagging/othertagsystems/comparetable.html) to compare Matroska fields with other common tags. This could be helpful too!

Something that might also be useful for thinking about embedded metadata is the [W3C Ontology for Media Resources 1.0](https://www.w3.org/TR/mediaont-10/).

Okay, that's all for now as I put together a final pull request and wait for review.
