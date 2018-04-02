---
layout: post
title: "Wild Wild Country and the Magnetic Media Crisis"
date: 2018-04-01 02:00:00 -0500
---

Wild Wild Country is a six-part documentary series from Netflix about the [Rajneesh Movement](https://en.wikipedia.org/wiki/Rajneeshpuram) and especially their attempt to build a utopian city in rural Oregon in the 1980s. To tell this story, the documentary relies very heavily on archival regional television footage and "home movie" footage. And, as countless people have noted, mostly look terrible. This is largely just the state of the tapes (your home movies also probably look terrible), but I did notice that there was a lot of aesthetic choices in finding some particularly eggregious errors and using them to push the narrative forward, like when something particularly dramatic happens (although the entire saga is quite dramatic overall!). 

I'm going to go through and point out some of the visual issues in this series and what causes them, referencing the [A/V Artifact Atlas](https://bavc.github.io/avaa/) when possible. One of the struggles when working with the AVAA is how to optimize for user search. The technical name for the problem is not always a descriptive name, and the point of the atlas is to be able to come to it with problems and learn what the correct terminology is, and how it might be corrected. I'll work towards making that better in the future.

I covered this before with Beyoncé's [Formation](http://bits.ashleyblewer.com/blog/2016/02/08/format-ion-video-playback-errors-in-beyonces-latest-music-video/) and [Lemonade](http://bits.ashleyblewer.com/blog/2016/04/29/lemonade/), and a bit for [Errol Morris's Wormwood](http://bits.ashleyblewer.com/blog/2017/12/28/errol-morris-wormwood-aspect-ratios/) but let's do it again for Wild Wild Country!

## Why does it look like this?

The footage is mostly a mix of 3/4" U-matic Tape (from public broadcasting) and VHS Tape (from amateur recordings). And in the first episode especially, lots of small-gauge ("amateur"/16mm) film.

### "Wiggy vertical lines"

![wwc](/images/wwc/1.jpg) 

The blurring on this opening shot, the first glimpse of archival footage in the show, is really interesting, I think. It's not so common to see repeating vertically-aligned ghosts of images. I would describe it as "vertical interlacing" but I know that'd be incorrect, because there is no such thing at vertical interlacing. Interlacing is the process of optimizing streaming video by having each frame show every other line, and that can cause the edges to jut out awkwardly. But it only runs horizontally. If this were MiniDV or DVCAM, this could be potentially diagnosed as [Banding](https://bavc.github.io/avaa/artifacts/head_clog_banding.html) but this is very likely VHS due to the low resolution quality and era. [This old forum from 2005](http://www.dslreports.com/forum/r14881779-Vertical-Interlacing) indicates its coming through the cable channel, and was likely appearing that way when it was recorded onto, presumably, a VHS tape.

### "Wiggy horizontal lines and shadows"

![wwc](/images/wwc/2.jpg) 

This is also VHS footage. The wiggly lines on edges running horizontally can be diagnosed as [Interlacing](https://en.wikipedia.org/wiki/Interlaced_video) issues, noticable especially between the windows of the schoolhouse. There is also some [Ghosting](https://bavc.github.io/avaa/artifacts/ghost.html) identified alongside the two people talking to each other on the far left of the screen.

### "Color shift especially at the bottom, blurriness"

![wwc](/images/wwc/3.jpg) 

The blurriness and inconsistent color patterns are a result of being VHS, and probably a VHS set to the super-long-play setting, stretching out the tape to fit the most amount of content on it, usually 6 hours, with a reduction in the video quality. Tapes that are re-used and dubbed over will begin to lose their fidelity and start to behave in this way as well. The off-coloring at the bottom is near where the "head" is could be from oxidation build-up, causing the color lock to fail more dramatically at the edge of the tape that sits closest to the head. I don't actually know but I do know when the video head gets clogged, [it causes these kinds of little lines](https://bavc.github.io/avaa/artifacts/video_head_clog.html).

### "High contrast, blown out clouds"

![wwc](/images/wwc/4.jpg) 

This excessively high contrast clouds is from video gain levels being up too high. This could happen during digitization and be locked into the image, or it could have happened when the image was created. The latter is more likely. For consumer-grade cameras especially, a quick shift from a low-light to excessive-light scenario will take some time to correct itself interally, to adjust to a better aperature (so in this case, it isn't so much the internal gain as it is the ISO of the camera doing the recording). An explainer for both is available [here](https://www.videouniversity.com/articles/what-is-the-difference-between-gain-and-iso/).

### "All together now"

![wwc](/images/wwc/5.jpg) 

A mix of many of the above errors can all be seen together in this handi-vac vacuuming red carpet for the arrival of Bhagwan Shree Rajneesh.

### "Lines near the top"

![wwc](/images/wwc/6.jpg) 

This is a very prominent error found on a lot of the 3/4" U-matic television footage. *I don't know what this is!* Do you know and can you tell me? It is essentially a chunk of several lines that repeat the previous chunk of lines immediately above it. It is more prominent in future episodes when the media gets more directly involved with the story.

Update! Thanks Dave Rice for these details, which I modified slightly from his message to me: “Lines near the top” is made by a TBC (time base corrector), basically it has a tiny digital buffer to hold a line and if the signal quality degraded too much, then it will release that buffer again and again. I have a dps575 and it outputs white vhs style speckle in that same place. I prefer the dps575 method since it looks more unprocessed."

### "Smudgy flashes of lines"

![wwc](/images/wwc/7.jpg) 

Especially in the early part of the series, there is some film footage too. This scene has some lines from film scratches and this frame shows a poorly-done amateur film splice to tape two pieces of film together during a cut. Some clips, especially of the group before coming to the United States, were originally shot on film and then migrated to an analog tape format, so we get to experience film scratches and fuzzy VHS dropouts at the same time!

### "Dark spots"

![wwc](/images/wwc/8.jpg) 

A quick tip for identification: film errors run vertically, up-and-down the frame, while video errors run horizontally, across the frame. 

### "White circles"

![wwc](/images/wwc/9.jpg) 

These white circles come from being at the end (or beginning) of a reel of film. They look nonsensical when played back, but they have meaning to the film processor -- they are an identifer for the batch of film used.

### "Glitches"

About 3/4ths of the way through the first episode, there is some general "glitching" used for dramatic effect. I don't know if this is one error that happened all at once with a tape or if it's a collection of several, but here are some frames from that incident for your enjoyment:

![wwc](/images/wwc/10.jpg) 
![wwc](/images/wwc/11.jpg) 
![wwc](/images/wwc/12.jpg) 
![wwc](/images/wwc/13.jpg) 
![wwc](/images/wwc/14.jpg) 


Okay, this is only the first episode. There are more strange errors to uncover and identify, but perhaps I will save them for a future post!

As always, please direct advice and corrections to the [Issues page](https://github.com/ablwr/ablwr.github.io/issues) or to [me directly](https://www.twitter.com/ablwr)!


