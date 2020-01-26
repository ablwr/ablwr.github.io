---
layout: post
title: "MediaInfoInfo: Video streams"
date: 2020-01-24 03:00:00 -0500
tags: [mediainfoinfo]
---

This is the fourth in a series of blog posts on a project I call "MediaInfoInfo". This project is focused on improving documentation for the ubiquitous media analysis tool [MediaInfo](https://mediaarea.net/MediaInfo). Wow, I can't believe another week has passed and I am due to write another blog post!

Previous posts:

1. [MediaInfoInfo: Initialize project](https://bits.ashleyblewer.com/blog/2020/01/10/mediainfoinfo-initialize-project/)
2. [MediaInfoInfo: Parameters / making a plan](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-parameters-making-a-plan/)
3. [MediaInfoInfo: General streams](https://bits.ashleyblewer.com/blog/2020/01/17/mediainfoinfo-general-streams/)

# Video!

Time to get into VIDEO! This is the heart of the entire library, along with the General stream that describes containers/wrappers. The Video definitions define the codecs, and that is where things can get really wacky.

I thought the Video stream fields would be really difficult, but there are a lot of fields that repeat themselves using different methods of displaying the associated measurements. It took some time to figure out what that pattern was, but after I did, it means using the same pattern for the 5 different ways to describe multiple fields, and that saved a lot of time. Also, a lot of fields were already covered by being the same as the General stream definitions, so I got to skip all of those. Here are some of the hightlights of my investigations while writing.

## Height and width

Height and width are things that seem simple but there are many ways in which it can be more complicated.

Large numbers are written in ["SI style"](https://physics.nist.gov/cuu/Units/checklist.html), used by most of the world but excluding the US. Uncareful programmers can run into a problem if they are trying to analyze based on numbers and not anticipate spaces in between, so it throws people off (I've seen this happen). I don't know that "SI style" is something broadly understood and of much use in the definition, but I can at least put it in there.

For height and width, the parameters note the consideration of aperture size. [Here](https://sourceforge.net/p/mediainfo/discussion/297609/thread/5651ab2d/?limit=25#2d51) is an example of the aperture size being implemented. Most of this fuss seems to come from Quicktime being totally weird about this stuff, and ProRes doing weird proprietry-ish things to make things more complicated for viewers that are not made exclusively by Apple. It can make a big difference, the pixel height and width and whether or not the playback mechanism is considering using the "production" aperture size or the "clean" aperture size. For some of the complexity around Quicktime files and how MediaInfo handles this information, [this writeup](https://sourceforge.net/p/mediainfo/discussion/297610/thread/d1c99d84/#98fa) breaks it down a bit, although notes "this may change in the future" from a posting six years ago.

This difference between the production aperture and clean aperture is described [here](https://lurkertech.com/lg/video-systems/#aperture), citing SPMTE RP 187-1995. To summarize, the "production" aperature is the absolute, full dimensions and the "clean" aperature is where it is okay to have the frame cut off for the presentation device. These terms are maybe industry standard, but I don't think they are particularly common. They were new to me, other than hearing complaints about the `clap atom`, I haven't really had to work with this. 

It is hard to phrase this succinctly in a small definition field, because it's a very complex topic that I haven't really spent a lot of time digging into. There's a lot there. That has been the pattern of me working through each of these definitions -- there is a whole lot to say and research into, but I'm taking the time to go deep enough to get an accurate definition and move on.

Dimensions weirdness doesn't stop there. There's also Stored height/width and Sampled height/width. Right now, I really don't know what these are about, but soon I will and can update the definitions accordingly. They don't really seem to be used, so I am curious.

## Scan types, orders

Scan types and scan orders seem to be an area of frequent confusion, according to the [MediaInfo FAQ page](https://mediaarea.net/en/MediaInfo/Support/FAQ#Analysis), which is otherwise sparse but makes room just for this.

Looking through the code helps, but there's also a wealth of information on Sourceforge, like [this question asked in 2016](https://sourceforge.net/p/mediainfo/discussion/297610/thread/f2459e8b/). Folks my age or younger may have forgotten that Sourceforge was the major code-hosting spot before GitHub became so ubiquitous, and there is a significant archive of discussions and technical support for MediaInfo and other projects. It'll be a huge loss when this site goes down (not that it has plans to go down, but all sites will die eventually).

ScanType and ScanOrder were also parameter fields that had no definitions, so I didn't have anything to go off of when creating the definitions, which is why I was reaching for some better understanding through the above sources. There are still some subfields that are a bit ambiguous to me and I am working through how to make them more clear, like `ScanType_StoreMethod_FieldsPerBlock` being more informative than something like "Count of fields per container block" (my working definition, which doesn't explain a lot). This will get a second pass later.

## MPEG format settings

Going through MediaInfo Video stream parameters, I ended up accidentally learning a bit more about specific encoding patterns found in the MPEG family of codecs, due to the many different format setting options. Here are some of them and links with more information (mostly just to wikipedia).
 
- [BVOP, PVOP, NVOP](https://forum.videohelp.com/threads/308081-bvop-pvop-nvop): I was aware of types of frames and their meanings, but not referred to in this way. Bidirectional, Predictive, and Null.
- [QPel](https://en.wikipedia.org/wiki/Quarter-pixel_motion): Hmm, "a quarter of the distance between pixels"? Sounds cool and grateful to the people who figured all of this out.
- [GMC](https://en.wikipedia.org/wiki/Global_motion_compensation): A pattern implemented for compression, again with the transforms.
- [CABAC](https://en.wikipedia.org/wiki/Context-adaptive_binary_arithmetic_coding): A way to achieve lossless compression, but also used in lossy compression


## Other things I didn't know much about

- [Multiview Video Encoding](https://en.wikipedia.org/wiki/Multiview_Video_Coding): This is for stereoscopic video (with multiple camera angles).
- [Active Format Description](https://en.wikipedia.org/wiki/Active_Format_Description): Some TV metadata!
- [Advanced Encryption Standard](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard): MediaInfo has a field for encryption information, but it is only implemented with this Rijndael block cipher standard.

There is more to say and think about regarding Video streams, but this is where I'm at right now. Next time, I will try to talk about what I find and learn about in the Audio stream parameters.

