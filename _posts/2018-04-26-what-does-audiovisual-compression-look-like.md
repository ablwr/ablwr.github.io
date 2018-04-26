---
layout: post
title: "What does audiovisual compression look like?"
date: 2018-04-26
---

This week, I'm thinking about this question: What does audiovisual compression look like? Can it be visualized? 

Turns out the answer is (update: meehhhhh?), and it's pretty easy to do, and it's actually not all that interesting. Y'know, *"It is different now exactly in places you expect."* But I wanted to stick with it and try to make it interesting anyway, so here is what I did.

TOP POST: I stick this down at the bottom vaguely but I want to point out that below isn't necessarily *compression* and can't accurately be asserted as such. A lot of things are happening other than changing codecs. This can speak to the extreme detail and care needed, and a thorough understanding required, that should go into making decisions based around long-term care of digital video objects, if that is the goal.

First, to get some pure data that hasn't been tainted with any particular flavor of encoding: enter [Big Buck Bunny](https://peach.blender.org/download/), everyones favorite signal processing test video.  

First, I had to cURL some Big Buck Bunny sample frames in order:   
```
curl "https://xiph-media.net/BBB/BBB-360-png/big_buck_bunny_[00400-00460].png" -o "#1.png"
```

Then I gathered those .png into a sample video file. I went with uncompressed v210 after [debating for a while](http://bits.ashleyblewer.com/blog/2018/04/25/uncompressed-versus-uncompressed-packed-video/).

The rest followed this pattern:


Cut that first video in this particular encoding!  
```
ffmpeg -i sample.mkv -c:v libx264 libx264-1.mkv
```

Loop 100 times more.  

```
for i in {1..100}; do ffmpeg -i libx264-"$i".mkv -c:v libx264 libx264-"$[i+1]".mkv; done
```

Compare the original with the 100th encoding and extract only the difference between the two into another video file.

```
ffmpeg -i sample.mkv -i libx264-100.mkv -filter_complex "blend=all_mode=grainextract" diff-default-libx264.mkv
```

I ran these: libx264 default profile, libx264 level 1 profile, prores, libx264rgb, libx265, vp8, vp9, a64multi, jpeg2000, dpx, mpeg1video, and wmv1.

Things I didn't do: Benchmarking (but jpeg2000 felt like it took forever!), processing power (but jpeg2000 also made my computer rev up! but maybe that was from me aggressively browsing Yelp for tacos on Firefox), keeping the 101th encode around for more analysis, run the results on the 101th encoding (you can see I run it on the 100th, whoops can't count).

So, what do we have? Let's cut thumbnails first:

```
for file in *.mkv; do ffmpeg -ss 00:00:01 -i "$file" -vframes 1 -q:v 2 "$file".jpg; done
```

And round them up:

## default-libx264  

![diff-default-libx264.mkv.jpg](/images/diff-default-libx264.mkv.jpg)  

## low-libx264

![diff-low-libx264.mkv.jpg](/images/diff-low-libx264.mkv.jpg)  

## libvpx-vp9  

![diff-libvpx-vp9.mkv.jpg](/images/diff-libvpx-vp9.mkv.jpg)  

## libvpx (vp8)

![diff-libvpx.mkv.jpg](/images/diff-libvpx.mkv.jpg)  

## mpeg1video

![diff-mpeg1video.mkv.jpg](/images/diff-mpeg1video.mkv.jpg)  

## libx264rgb

![diff-libx264rgb.mkv.jpg](/images/diff-libx264rgb.mkv.jpg)  

## dpx 

![diff-dpx.mkv.jpg](/images/diff-dpx.mkv.jpg)  

## prores

![diff-prores.mkv.jpg](/images/diff-prores.mkv.jpg)  

## jpeg2000

![diff-jpeg2000.mkv.jpg](/images/diff-jpeg2000.mkv.jpg)  

## libx265

![diff-libx265.mkv.jpg](/images/diff-libx265.mkv.jpg)  

## wmv1

![diff-wmv1.mkv.jpg](/images/diff-wmv1.mkv.jpg)  

As someone who runs around a lot in mostly digital preservation circles, I think I'm most surprised by what comes out of the prores and jpeg2000 encodings, and also the ways in which they are different. DPX too, shows something.

I think the differences between VP8 and VP9 are really interesting, especially around the edges. I'm also surprised at how little mpeg1 and wmv1 changed compared to more renowned codecs. And the difference (or lack of) between h264's default high-quality encoding compared to the lowest level.

This is just a cursory analysis and while I followed loosely some scientific principles in terms of consistency of chosen source material, this is far from scientific. `ffmpeg` is known for doing things "under the hood" that may be unanticipated or unexpected by its user, like switch up the colorspace or make other assumptions, especially based on the container format. 

Also, I tried to run the DV video encoder as well, but I just got a totally blank result even though I was confident that compression was happening. And I tried to run the process on a64multi, defined as "Multicolor charset for Commodore 64", but it broke after 3 tries, twice, and the files wouldn't open, so I guess it was just not meant to be.

Also, this was essentially done back in 2012 by expert preservationist Dave Rice using a different ffmpeg technique, you can read his results [here](http://dericed.com/2012/display-video-difference-with-ffmpegs-overlay-filter/) although the videos are no longer up.
