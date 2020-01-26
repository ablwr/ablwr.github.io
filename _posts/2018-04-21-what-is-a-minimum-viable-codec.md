---
layout: post
title: "What is a Minimum Viable Codec?"
date: 2018-04-21
tags: [recurse center, codecs, video]
---

It's my third week at the Recurse Center and this question has been on my mind. What is a minimum viable codec? (And what is the least amount of work I could do to successfully create a codec?)  

Well, what is a codec, exactly?  

To be totally obvious and unpack the portmanteau, it's a coder/decoder.

- Coder: encodes a data stream or a signal for transmission and storage
- Decoder: reverses the encoding for playback or editing


Fortunately I found the [World's Smallest h264 Encoder](https://cardinalpeak.com/blog/worlds-smallest-h-264-encoder/) and the associated [code repository](https://github.com/archersmind/H264Experiment), which I forked and ran with the provided sample data stream.

There is also advice on making one's own raw stream of data, which I did like this:  

`ffmpeg -f lavfi -i mandelbrot=size=100x100:rate=25 -s sqcif -pix_fmt yuv420p -t 20 test.yuv`

...making a YUV colorspace 4:2:0 chroma subsampled progressive-scan uncompressed video file of a mandelbrot, with the `-s` flat set to `sqcif`, a [Common Intermediate Format](https://en.wikipedia.org/wiki/Common_Intermediate_Format) short for "Sub Quarter CIF" that can be easily manipulated by encoders and muxers.


The code seemed to work -- it didn't throw errors. But just like the input is a raw stream of data, the output is also a raw stream of data. To find out, I had to wrap the stream by muxing it into a wrapper. I chose MKV because it would be the best for debugging, as an open standard, but any wrapper should work just fine:

`ffmpeg -f h264 -i test.264 -vcodec copy test.mkv`

This is great because in addition to understanding this whole *MVCodec* thing, I've been trying to think about what it means to be a raw stream of data, and what that looks like, and what qualifies as raw data. This mini-project gave me ample opportunity to dig deep into binary and hex and to think about writing header data and frame data and all the bytes that make up parts of a video file. At the higher level, I've been thinking about where "uncompressed" falls in all of this. "Uncompressed" still has parameters set into it, most notably something like chroma sub-sampling. Like I mentioned in [a previous blog post](http://bits.ashleyblewer.com/blog/2018/04/03/exploring-codecs-and-data-streams/), there isn't just one kind of uncompressed data, and it has essentially been encoded into something in order to determine how much chroma data should be kept. Unless at 4:4:4(:4), even uncompressed is still going to be encoded and still going to be lossy, just in ways that are not perceptible to human eyes. Nearly all stream transformations are going to have some sort of loss.

Anyway, I stopped philosophizing and starting writing code. I didn't get much farther than renaming stuff from C and into Rust before I paired up with Brad and Rory. Brad didn't last too long because while pairing is a great programming task, any amount more than two is like this "programming by committee" bizarre zone (and we didn't have one shared screen). But Rory stuck with it and was super kind, and wrote most of the code and figured out what needed to happen to get things compiling, and I am very grateful. Also, he picked up Rust only like three days ago and is already a lot savvier than I am. A lot of the benefit of pairing with other people is less about the two-people-solving-one-problem-better but learning unanticipated things, like about how his [VSCode](https://code.visualstudio.com/) extension for Rust will help catch compiler errors pre-emptively and also help with syntax, which are all the things I'm struggling with heavily trying to get my brain wrapped around just typing out code.

Something I really liked about this mini-project was that when our code was working but producing non-expected results, we got a lot of `ffmpeg` errors when trying to mux our data mess into a file. 

Here's what we got when we weren't adding the microblock header:

```
[h264 @ 0x7ffb7e813200] top block unavailable for requested intra mode -1
[h264 @ 0x7ffb7e813200] error while decoding MB 1 0
[h264 @ 0x7ffb7e813200] concealing 48 DC, 48 AC, 48 MV errors in I frame
```

Here's what was going on when we weren't adding a bit to close out the slice data:

```
[h264 @ 0x7fc616003e00] Not enough data for an intra PCM block.
[h264 @ 0x7fc616003e00] error while decoding MB 7 5
[h264 @ 0x7fc616003e00] concealing 48 DC, 48 AC, 48 MV errors in I frame
```

As we were close to wrapping up, someone else starting in on their own version, which was looking like it was shaping up to be a very well- refactored version of what we had managed to produce. I got distracted by someone else who was just hinting at possibly wanting to understand a video file's structure, so I rushed away to talk about that and try to convert someone else to the Video-is-Great fan club. But I'm still happy with our verbose output and I feel it honors the original C code. Also, I'll refactor it later, especially the part where we hardcode the `filesize` and `filename` and make it impossible for anything else to be run. But I'm happy to have produced some code that answers my question: this is truly the MINIMUM VIABLE CODEC. Except, you know, the part about decoding. But that is for another week!

I almost forgot: If you are curious about this, we checked the code and sample datastream into github so you can try it yourself [here](https://github.com/ablwr/hello264-rust).