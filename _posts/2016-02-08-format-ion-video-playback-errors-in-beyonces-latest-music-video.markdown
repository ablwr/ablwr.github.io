---
layout: post
title: "Format-ion: Video playback errors in Beyoncé’s latest music video"
date: 2016-02-08 20:19:34 -0500
tags: [beyonce, avpres]
---

Update: There are a few other blog posts in this series --
- [Aspect Ratios in LEMONADE, Pt. 1](https://bits.ashleyblewer.com/blog/2016/04/29/lemonade/)
- [Aspect Ratios in LEMONADE, Pt. 2](https://bits.ashleyblewer.com/blog/2016/05/24/aspect-ratios-in-lemonade/)
- [Beyoncé's HOMECOMING: Film, film, and video](https://bits.ashleyblewer.com/blog/2019/04/29/beyonces-homecoming-film-film-and-video/)

Like most people I know, I spent most of yesterday watching "[Formation](https://www.youtube.com/watch?v=LrCHz1gwzTo)" over and over, and noticed Beyoncé really has a thing for faking media playback errors for some reason. And this new digital drop covers many errors and several formats all in one. You can also watch things get digital-ailments-buckwild in the video for [Grown Woman](https://www.youtube.com/watch?v=y3MjxWn5W9M), which mixes real home movies (that have real analog video problems) with the modern-day, grown-ass Beyoncé who has a video visual effects team to make things look bad on purpose.

But... what are those problems, how are they caused, and how do you avoid them? Ladies, let's get in( )formation!

# Film

I’m going to move through the video by format chronology, rather than video playback runtime. Film is the easiest to diagnose and oldest media format, and I saw a couple of (computer-generated replications of) errors rear their ugly heads! Let us slay.

## Light leaks

<img src="https://j.gifs.com/pY2n5m.gif"/>

This fuzzy, overwhelming red is due to the way film is/was created by [specific exposures to light](http://www.lomography.com/magazine/260270-creating-light-leaks-the-analogue-way). If light enters the camera during the filming process, the underlying emulsion on which the images are stored is washed out and this sudden, excessive exposure to light is interpreted on film as a red glare. In a few shots, the fake light leaks in this video are a bright teal, which is unrealistic. Changes in hue other than red are more likely to occur in video playback. This error is unpredictable and occurs before the film has been developed, which is a chemical process that turns the negative image into the expected image that is then projected on a screen.

## Dirty/scratched film

![](/images/bey/filmtear.png)
![](/images/bey/greenlines.png)

There are a few fake "film scratches" in the video, some of which are more realistic than others. There’s a subtle, white, vertical scratch added in one scene, which looks a lot like a real scratch caused from a large particle caught during a film being projected. There’s also a few scenes of added, irregular horizontal scratches that are bright green. These horizontal scratches happen, more likely during the handling process than through wear & tear of a machine, but it’s not expected for them to be a bright neon green (but not impossible, just improbable). Film scratches are usually vertical because it comes from being played on dirty projection equipment. Video scratches are horizontal because of the way they are played back. If the bright green "scratches" were less curvy, they might look more like a scratch on a video tape.

## Blurriness

![](/images/bey/blur.png)

Blurriness is caused here by a post-production filter but could be caused from poor tension between the film and the projector or from the lens moving out of focus, the latter being a problem regardless of the format.

# Video

## Sync issues..?

<img src="https://j.gifs.com/G68xRQ.gif"/>

This is a computer-generated replication of "video going wild" so it's hard to pinpoint exactly what's wrong, but if you see this, it's probably some sort of tracking and skewing error generated (when occurring naturally) by some breach in communication between the magnetic tape and the device which is playing it back. This can be seen in consumer decks when stopping the tape abruptly, causing a disconnect of the magnetic signal and release of the tension between the tape and video head drum. Or maybe through messing with bad cords. Or maybe someone [stuck a damn magnet](https://www.youtube.com/watch?v=_yEu2R1gYSs) on top of the tv [again](https://www.youtube.com/watch?v=rO_lwjhoSiU).

![](/images/bey/video.png)

## Lines

![](/images/bey/coordination.png)

Analog video has a much, much lower rate than modern digital video (and thus, modern monitors where video is played back), which means each individual line is visible. You can think of the lines as pixels — something I no longer see using a Retina Macbook but barely visible on older machines, and very visible on much older machines. When seeing a low-resolution standard definition video transmission cut in between HD video, it’s more obvious.

(Also the "Play" text is looking a little wobbly here, maybe too much playback of a consumer-grade tape or you should clean the VHS heads on your deck?)

![](/images/bey/hotmess.png)

It’s also more obvious when it’s just a fake filter, which is the case here, but whatever. You can see in the image above that it doesn’t have the same line problem as in other clips even though they are meant to be part of the same tape. The above image is also an example of the applied ghosting as well as an oversaturated image, resulting in whites that appear "blown out" and a lack of true, rich black tones. There’s also some interlacing going on, which we’ll get to next.

## Interlacing

![](/images/bey/interlacing.png)

Interlacing issues can be seen during movement, where squiggly lines appear in places of motion. The concept of interlacing involves each frame containing 50% of the line information required for a full picture, and having even and odd frames play back half of the information quickly enough would result in a full-looking image. This was done because it was faster to send video signals, like in the case of television, when this kind of technique is used. Now it just lingers around making everything look like garbage. There’s a good summary devoid of sentimental feelings available on [Wikipedia](https://en.wikipedia.org/wiki/Interlaced_video) though.

## Ghost image

![](/images/bey/ghosting.png)

When a video signal, during transmission, is not properly balanced, it will cause a shadow-like image either to the right or left of the primary image. Softer secondary signals are created and [cause this effect](http://avaa.bavc.org/artifactatlas/index.php/Ghost). If dealing with an analog asset, make the video deck "prove to you that it got some coordination" by using a [time-based corrector](https://en.wikipedia.org/wiki/Time_base_correction) and the ghost image should go away. If dealing with a digitized analog video, it is already burned into the digital stream upon transmission and the results are permanent (which is why getting the highest quality stream during analog-to-digital migration is so important).

This is similar to the issue of [image lag](http://avaa.bavc.org/artifactatlas/index.php/Image_Lag) which appears in video formats older than this one is intended to be (which is probably VHS). This is also maybe how the world looks if you follow Mrs. Carter's advice a little too hard and you're sippin' Cuervo with no chasers.

## Drifting bars

<img src="https://j.gifs.com/v2Z5yV.gif"/>


Sometimes a fuzzy, faded bar will appear to move across the image, which is caused as the tape begins to become worn out from being played so frequently, and possibly on low-grade or not-regularly-cleaned machines. This is kinda faked during the digital intro, which is just weird.

![](/images/bey/digibars.png)

## Dropout

[Dropout](http://avaa.bavc.org/artifactatlas/index.php/Video_Dropout) is such a common video error! It's practically "that video feeling"! Anyway, it’s caused by the wear and shedding of the magnetic particles on tape, which come from playback or just from long-term exposure to oxygen, dirt particles on the tape, poor environments, and tape mishandling. It's kinda sprinkled in during the video segments but hard to really pinpoint other than during the "sync issues" section above. It shows up a lot in "Grown Woman" though (and in LIFE)!

## Low res

![](/images/bey/lowres.png)

Okay, we know fair Victorian Beyoncé and friends scenes were filmed with a standard HD camera, but for just a second there’s a low-resolution version of it at the 2:45 mark. Why? Why? Anyway, this is what things look like when filmed on a crappy, cheap camera. Again, the lightest part of the image is blown out, which leaves a blue shadow around the silhouette in the (relative) foreground. Also the [aspect ratio](https://en.wikipedia.org/wiki/Aspect_ratio) looks weird.

# Digital

## Digital screens

![](/images/bey/digital.png)

Finally, don’t forget about digital video! The only intentional errors are at the beginning of the explicit version of the song, where a warning is typed on a screen that has been recorded with (presumably) a digital video camera. If you’ve ever pointed any kind of camera to a monitor, you’d notice that its refresh rate is not in sync with the rate of which images are captured on video, which results in a kind of visualized representation of what human eyes can’t naturally see: [the screen refreshing itself](https://en.wikipedia.org/wiki/Refresh_rate). In this, you can see very small lines as well as a band that moves quickly in an upwards movement. Very old monitors would have a slow band move downward across the screen, according to a video recording. Modern computers refresh at a much quicker rate, which results in these light bars that resemble the video lines mentioned above.

## "Glitching"

<img src="https://j.gifs.com/o2yKVN.gif"/>

Some more "glitching" occurs in this scene (pixels becoming more focus and changing colors, blurred text, ghosting) but it’s not representative of something that would occur naturally on the screen or within the camera, just a cheap effect. Some of it sorta looks like its imitating a flickering from an electricity surge. Anyway, digital video glitching drives me crazy both in a professional context (because I slay) AND because I think it's wack (also because I slay).

## Codecs

![](/images/bey/fakecodec.png)

There is another digitally generated "glitch" that I think is trying to capture the feelings of a clogged video head, but could theoretically be similar to a codec error that would leave a black bar temporarily over a portion of the screen on a per-frame or chunked-frame basis.

# Conclusion

Anyway… one video, three generations of moving images. Remember all of these issues are a lot more likely to happen if you do dumb things like keep hot sauce in your bag (video preservation swag bag) so follow good media-handling practices. And remember if Beyoncé’s childhood home movies are suffering, what about yours? Please consider migrating to a safe digital surrogate as soon as you can, if you can afford to do so.

PS: Hello, video preservationists. I posted this somewhat in haste (aka this isn't a damn whitepaper, y'all, it's a blog post), so please direct advice and corrections to the [Issues page](https://github.com/ablwr/ablwr.github.io/issues) or to me directly! I like collaboration more than fact-checking myself thoroughly out of fear of embarrassment. Get on this level and submit a pull request!

Special thanks to [BAVC](https://bavc.org/) for creating the [A/V Artifact Atlas](http://avaa.bavc.org/artifactatlas/index.php/A/V_Artifact_Atlas), a free, open, and invaluable resource for the identification of video errors.