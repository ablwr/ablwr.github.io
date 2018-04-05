---
layout: post
title: "Exploring codecs and data streams"
date: 2018-04-03
---

`ffmpeg -codecs | grep "things I have heard of"`

Guide to codecs when presented by FFmpeg:  

```
Codecs:
 D..... = Decoding supported
 .E.... = Encoding supported
 ..V... = Video codec
 ..A... = Audio codec
 ..S... = Subtitle codec
 ...I.. = Intra frame-only codec
 ....L. = Lossy compression
 .....S = Lossless compression
 -------
```

Types of uncompressed data supported by FFmpeg (at least):

```
 D.VI.S 012v                 Uncompressed 4:2:2 10-bit
 DEVI.S avui                 Avid Meridien Uncompressed
 DEVI.S ayuv                 Uncompressed packed MS 4:4:4:4
 D.VI.S frwu                 Forward Uncompressed
 D.VI.S m101                 Matrox Uncompressed SD
 DEVI.S r210                 Uncompressed RGB 10-bit
 DEVI.S v210                 Uncompressed 4:2:2 10-bit
 D.VI.S v210x                Uncompressed 4:2:2 10-bit
 DEVI.S v308                 Uncompressed packed 4:4:4
 DEVI.S v408                 Uncompressed packed QT 4:4:4:4
 DEVI.S v410                 Uncompressed 4:4:4 10-bit
 DEVI.S y41p                 Uncompressed YUV 4:1:1 12-bit
 DEVI.S yuv4                 Uncompressed packed 4:2:0
```

It would seem like uncompressed is just uncompressed, but there are (minimally, by-default) 13 different forms of uncompressed data that can be decoded and mostly encoded by FFmpeg. So just because something is uncompressed doesn't mean that it is raw data or lacking in some sort of algorithm. 

Self-citing refresher on the meaning of these numbers, which are chroma subsampling: [http://training.ashleyblewer.com/presentations/video.html#23](http://training.ashleyblewer.com/presentations/video.html#23)

## What does "Intra frame-only codec" mean?
Intra frame only codec is something that concerns itself only with analysis within the current frame, not in relation to other adjacent (or non-adjacent) frames. Lossless codecs are lumped into this "intra frame-only codecs" category by default, I presume, just because they aren't manipulating the stream at all and they are definitely not the opposite option in this dichotomy: "inter-frame prediction frames". So, intra frame coding is going to only mess with what's in the frame, and inter-frame (prediction) is going to check out its neighbors.

- Intra-frame: limited to frame   
- Inter-frame: compression with one or more neighboring frames  

This will be important later in my future.

## Pictures, frames, fields, slices?

Gahhh! This is the point in the day where I thought I understood things and now feel like I don't. Groups of pictures, frames, fields, slices. But then I went through it all and now I feel like I do.

## Groups of pictures (GOPs)

Does exactly as it sounds, groups a bunch of frames in a logical way, or based on size, or whatever is decided on. It helps speed things up -- the decoder doesn't have to worry about any frames that are not inside of the GOP to which it belongs to.

## Lossless video as many individual image files 

I can see the reason why preservationists choose JPEG2000 or DPX for their moving image files, especially with the history of starting with film -- they are literally a picture for every frame, resulting in zillions of little files that can be played back as one moving image, which is also how film works, frame-by-frame.

Analog and digital video have frames toooooo, obviously something has to keep things all wrapped up, but conceptually I don't think of them as frames in the same way, I think of like an old old CRT monitor that slowly draws lines and then decides to start over, and when it starts over, that happens to be a new frame, moving through time. Digital videos have frames too, sometimes based in time. When digital video is compressed with an algorithm using inter-frame techniques, some of the compression may be pointing to other frames instead of living all alone and repeating within the data stream, so the frame is there but it is partial in some ways. Keyframes are created at drastic change points in which data can be hinged off of.

- I‑frames don't use other frames to decode
- P‑frames use previous frame data to decode 
- B‑frames uses previous and next frame data to decode 

## Fields 

Turns out when interlacing gets involved (I will forever hate it as a trouble-causing ancient compression algorithm), odd- or even-number sections can be defined as fields, and with interlacing, two fields equal one frame. A field is like half the image and presumably has a pair out there, also presumably right next to it. But not necessarily a pair.

*Thanks Joshua Ng for the correction made here: I meant as stated above, not "two frames equal one field" as previous stated.*

## Slices

Slices are distinct parts of a frame. Like if you wanted to divide the frames up into four.

So, in conclusion, video is hard. But. Groups of pictures have frames. Frames can have fields. Frames can be broken into slices. I think I have a pretty good understanding of what's going on here, and now I need to start working towards actually manipulating this stuff!


Resources:
[http://users.cs.cf.ac.uk/Dave.Marshall/Multimedia/node248.html](http://users.cs.cf.ac.uk/Dave.Marshall/Multimedia/node248.html)  
Wikipedia is also really good about detailing all the above  
