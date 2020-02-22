---
layout: post
title: "MediaInfoInfo: General streams"
date: 2020-01-17 03:00:00 -0500
tags: [mediainfoinfo]
---

This is the third in a series of blog posts on a project I call "MediaInfoInfo". This project is focused on improving documentation for the ubiquitous media analysis tool [MediaInfo](https://mediaarea.net/MediaInfo). After the [initial project idea](https://bits.ashleyblewer.com/blog/2020/01/10/mediainfoinfo-initialize-project/) and [initial project plan](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-parameters-making-a-plan/), this post will focus on work on the first and largest section of parameters: the General stream.

Other posts:

1. [MediaInfoInfo: Initialize project](https://bits.ashleyblewer.com/blog/2020/01/10/mediainfoinfo-initialize-project/)
2. [MediaInfoInfo: Parameters / making a plan](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-parameters-making-a-plan/)
3. MediaInfoInfo: General streams
4. [MediaInfoInfo: Video streams](https://bits.ashleyblewer.com/blog/2020/01/24/mediainfoinfo-video-streams/)
5. [MediaInfoInfo: Audio streams](https://bits.ashleyblewer.com/blog/2020/01/31/mediainfoinfo-audio-streams/)
6. [MediaInfoInfo: Image, Menu, Text and Other streams](https://bits.ashleyblewer.com/blog/2020/02/07/mediainfoinfo-image-menu-text-other-streams/)
7. [MediaInfoInfo: MediaInfo-specific words](https://bits.ashleyblewer.com/blog/2020/02/14/mediainfoinfo-mediainfo-specific-words/)
8. [MediaInfoInfo: Metadata Tags](https://bits.ashleyblewer.com/blog/2020/02/21/mediainfoinfo-metadata-tags/)

The General stream summarizes the container information for a file. Sometimes this is known as the wrapper. And sometimes, this is assumed to be all the information about a file because it conveys what the file extension will be. But it doesn't give information from any of the codecs inside. Containers are all different -- some are very assertive and can contain a lot of information that influences how the file plays back, and others are very open and leave those decisions to the codec. Sorry -- it's complicated and can be hard to summarize so breezily!

Here are some highlights and painpoints from me going through all of the parameters for the General stream in MediaInfo. Many of these are applicable to all of the streams, but this is where I am first encountering them and want to get the definitions in a strong place, since they will eventually be repeated across the other streams.

## Count and Status
 
 After floating around for a bit in the definitions, the first thing I settled on tackling was the first field in the first division I was working in, General. Although this field and several of the following are defined in all of the groupings. The definition is initially straightforward: "Count of objects available in this stream". But then I was thinking -- What is considered an "object"?

 Already, I am jumping into the code base. That's good, because a side goal for me is to get more comfortable reading C++.

 "Count" doesn't appear in the standard MediaInfo output, only with the Full option (`-f`). Running through a few files, the Count value is consistently in the range of 331 with maybe a couple more, and Audio streams are 280 with maybe a couple more, Image streams are 124 with a couple more... so my instinct here is that the objects referred to in Count are C++ objects, and I am going to update the parameter definition to reflect that and be glad that this will go through a code review process.

 The next parameter is Status, defined as "Status of bit field (0=IsAccepted, 1=IsFilled, 2=IsUpdated, 3=IsFinished)." This also, to me, seems to be for internal use and I will have to verify that. "Count" and "Status" are both vague terms that are hard to search through a codebase with, although the less-common values (IsAccepted, et al) indicate this on top of the definition itself implying this is the status set while the parser is parsing.

## Base what?

 Next are parameters that are easier to work with and I don't have to guess at their true meanings. Things like `StreamCount` and `StreamKind`. The only issue I am thinking through here is the use of (base=0) and (base=1) to indicate if the numbers are going to increment starting at 0 or starting at 1. "base=1" makes sense, and it definitely makes sense to computer programmers -- but people that are not programmers usually aren't even aware that counting could start at zero instead of of one. I am going to request that the sparse (base=1) gets replaced with "Counting starts at 1." I'm not yet convinced that this is absolutely the best way to phrase this, but it's the best I have at the moment. It has me thinking about when to define a technical term, and when to realize that trying to explain it might make it more confusing to people who are likely to understand the technical term? I'm thinking especially of when English is not someone's first language, and English is understood in the context of being the de facto language for doing programming work.

The next few went well enough, and there were plenty of deprecated options that didn't need changing. In a perfect and well-funded world, it would be worth taking the time to describe these legacy options and what they do, but that's not the case here so I moved forward.

## File size measurements

File size counts were the next big pausing point. The first is well-described as "File size in bytes" and the rest are like this last one: "File size (with measure, 4 digit mini)." I can guess what these represent when I see them, but it's harder to explain them. Plus, there's the difference between file sizes defined based on different orders of magnitude.

```
File size                                : 1800920
File size                                : 1.72 MiB
File size                                : 2 MiB
File size                                : 1.7 MiB
File size                                : 1.72 MiB
File size                                : 1.717 MiB
```

MediaInfo measures file size data in the officially standard accepted format of measuring by powers-of-1024. Unfortunately, big computer companies have dominated the cultural understanding of how to size data and measure things based on the powers-of-1000 to make things seem bigger, and it just makes things unnecessarily confusing. So I think it's worth being more explicit about the way MediaInfo is sizing things, just to have to counter this baseline understanding and perhaps eventually lead people to understanding why 1800920 bytes is 1.72 MiB.

I referenced the definitions of human-readable sizing from `df`, a small command-line tool that knows about measuring disk space. `df` defines its `-h` flag as "print sizes in powers of 1024 (e.g., 1023M)" and `-H` as `print sizes in powers of 1000 (e.g., 1.1G)`. I had to think for a while about this, lurking wikipedia pages for [floating points](https://en.wikipedia.org/wiki/Floating-point_arithmetic) and [binary prefixes](https://en.wikipedia.org/wiki/Binary_prefix#Deviation_between_powers_of_1024_and_powers_of_1000), because I want to be precise, use the most widely acceptable language, and still be easy to understand to people who spend most of their time in the world of decimal-based counting. When I see something like "1.01", I read that in my head as "one, decimal point, zero one" and I would describe the far-right 1 is in the second decimal place, but that all gets thrown out the window when things aren't being counted in base-ten anymore.

"File size with human readable measurement (measured in powers of 1024) rounded to three floating points" also isn't right. I was looking for the word "radix" to describe what I have always just called the "decimal point" but I suppose could be the "binary point."

## Duration

Duration is another thing that is pretty straightforward until there's seven different options that need their differences articulated. I'm used to the HH:MM:SS:mmm syntax, and what it means to read things in milliseconds, but I wasn't sure what `XXx YYy` should stand for, in the original documentation. I determined through testing that it is the numbers and values, like "1 hr 30 min" or whatever the appropriate duration is, and had to think about how to represent that.

Another difficult one was "Play time in format : HHh MMmn SSs MMMms, XX omitted if zero" because I am not sure what the `XX` means in this context, and I will have to confirm if this just means that it will not show any of the potential fields if they are empty, and how to properly articulate that, too. 

There are also parameters for `Duration_Start` and `Duration_End` that have no definitions at all. Given where these get used in the codebase, it seems to be used for [MPEG transport streams](https://en.wikipedia.org/wiki/MPEG_transport_stream) and, also based on the code, are expected to come out of the system as [UTC](https://www.timeanddate.com/time/aboututc.html). So, some things need to be defined for the first time.

## Metadata fields

Metadata tags opened up a whole can of worms with their own additional resources and definitions. Should I note that these fields are derived from metadata tags? Should I go even farther and note if they are coming from specific types of fields (like ID3v2)? Will that change in the future? Are these a mix of fields derived from metadata tags and also from other analysis? I had to check each individually to find out, and I am sure there will be some confusing issues that I'll need to revisit when I go through a second, third, fourth pass.

## A few other areas of research

The overall bit rate mode comes in two flavors: as an acronym and as the word. And overall, this category is fine, but will get more complicated when out of the General stream and looking at the Video and Audio streams.

There was a whole category that had no definitions associated with it, and that is the `ServiceName` category. Through some research and context, I understood these to be a section dedicated to assisted services, such as voice-over or commentary for the visually impaired associated with the General container.

Something new to me were two parameters with no definitions that detailed [Electronic program guide](https://en.wikipedia.org/wiki/Electronic_program_guide) data. I have used these but I've never thought about what kind of data might be found in the container, or how that might be displayed in MediaInfo (in this case, the beginning and ending positions).

Those are some of the larger things I had to think through and learn about while going through the containers portion ("General") of these MediaInfo parameters. Next up will be VIDEO!