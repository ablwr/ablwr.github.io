---
layout: post
title: "Uncompressed versus uncompressed packed video"
date: 2018-04-25
tags: [recurse center, video, ffmpeg]
---

I'm thinking more ([previous post](http://bits.ashleyblewer.com/blog/2018/04/03/exploring-codecs-and-data-streams/)) about uncompressed encoding options and the information they convey and how they convey it. For something else I'm working on (update, [here](http://bits.ashleyblewer.com/blog/2018/04/26/what-does-audiovisual-compression-look-like/)), I am trying to get an extremely neutral original format that I'll be encoding, so I wanted to understand better these flavors of uncompressed that I have to choose from:


```
 V..X.. avui                 Avid Meridien Uncompressed
 V..... ayuv                 Uncompressed packed MS 4:4:4:4
 V..... r210                 Uncompressed RGB 10-bit
 V..... v210                 Uncompressed 4:2:2 10-bit
 V..... v308                 Uncompressed packed 4:4:4
 V..... v408                 Uncompressed packed QT 4:4:4:4
 V..... v410                 Uncompressed 4:4:4 10-bit
 V..... y41p                 Uncompressed YUV 4:1:1 12-bit
 V..... yuv4                 Uncompressed packed 4:2:0
```



I've already thought out the differences between 4:4:4, 4:2:0, 4:2:2, etc... 

But now, something I got stuck on is how some of the above say they are packed and some of them do not say anything about that. Also some say 4:4:4:4 and some just say 4:4:4, but I am assuming that the last :4 is implied present, since its the alpha channel and AFAIK it is always sampled every time, no sub-sampling going on because that'd be weird, and it'd be a weirdness worth noting.

When looking this up, I got momentarily sidetracked because Xvid has a packed bitstream, but that is referring to the way it handles the order of frames (I-Frames, B-Frames, P-Frames). You can see this old blog post [here](http://itsjustonesandzeros.blogspot.com/2007/01/what-is-packed-bitstream.html) about it. This may be useful to people these days (or in the future) working with video made in the 2000s, but is not related to the current concerns.

Anyway, I was stuck on this whole "packed" thing. What is packed? What does it mean to be packed? Are the others unpacked? Uncompressed packed sound contradictory???!!!

My first assumption was that if some are packed, the others therefore must be unpacked, but that isn't the case. 

[FourCC](http://www.fourcc.org/yuv.php#Packed%20YUV%20Formats) explains this very succinctly:  

"YUV formats fall into two distinct groups, the packed formats where Y, U (Cb) and V (Cr) samples are packed together into macropixels which are stored in a single array, and the planar formats where each component is stored as a separate array, the final image being a fusing of the three separate planes."

I like thinking about these by writing out the arrays:  

```
planar = {[yyy], [uuu], [vvv]}  
packed = {[yuv], [yuv], [yuv]}
```

So just like `:4` is implied, uncompressed encodings (dare I call them that? I'm still thinking that through.) are assumed planar encoded unless noted otherwise. 

Macropixels: But also yeah, what's a macropixel? This gets into pixel formats.

You can list all the pixel formats supported by ffmpeg with `ffmpeg -pix_fmts`. There are a lot! What is a pixel format? A pixel format is a standard predefined way to store pixel data. Since pixels have to consider the Y and U and V (or whatever is being used), those can be represented in different ways. This seems to usually be described as pixel "components." I've seen "SubPixels" used in libraries too. Components is good, because you know that each component is needed to make up one whole pixel. 

So, pixel formats! FourCC says UYVY is "probably the most popular" for YUV 4:2:2. [Here](http://www.fourcc.org/pixel-format/yuv-uyvy/) is their page on YUV UYVY. It's YUV 4:2:2 arranged with a Y sample at every pixel and U and V sampled at every second pixel horizontally on each line and the style is packed. This way of arranging pixel data uses macropixels, which is just to mean that it "packs" two parts of the pixel data into one byte (which is an unsigned 32-bit integer, I'm not gonna go into that though, this is enough). I don't really care that they are cohabiting in the same byte but I guess if you are in the business of collecting pixel census data, then maybe you could care. This doesn't seem to save much space either way, and possibly takes more time to encode/decode. But also these opinions are at such a low level and both have well-understood ways to decode, so I am happy not worrying about it too much.. for now.

Okay, so this is all for my quest of getting some seriously neutrally uncompressed data that is acceptable by even snobby codecs that only work with specific chroma subsampling patterns (looking at you, DV!).

A final thing: I'd be remiss if I didn't mention `-c:v rawvideo` as an option but my source, the much-loved Big Buck Bunny, is RGB and I want to be working in the YUV realm, but I suppose that really is the purest of pure.

Oh, also, the [LC Sustainability of Digital Formats Guidelines](https://www.loc.gov/preservation/digital/formats/fdd/fdd000352.shtml#notes) has some useful notes on this as well that took me multiple read-throughs before I understood it, even though the hardware implications of these things have been on my mind also. I've been so impressed with the wealth of information found in this underutilized resource!

As always, [let me know if I'm wronggggg](https://twitter.com/ablwr)!