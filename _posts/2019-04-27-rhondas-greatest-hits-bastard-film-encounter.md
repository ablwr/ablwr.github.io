---
layout: post
title: "Rhond<3's Greatest Hits"
date: 2019-04-20 02:00:00 -0500
tags: [web preservation, video, ffmpeg, conservation, conferences]
---

![rhonda](/images/rhonda3.jpg)

Sometime between the time of me writing and this and me posting this, I will be
presenting with my colleague [Travis L. Wagner](http://travislwagner.com/) at
the [Bastard Film Encounter](http://bastardfilmencounter.com/), a film symposium
rejoicing in media that is "ill-conceived or received; embarrassing or beyond
the bounds of acceptability; poor in conception or execution; undesirable to
those who should be caring for them; proof of something that should have never
happened."

The symposium is primarily based around a love of film and of archiving, but
Travis and I are exploring the preservation of the near-present, which is
dissipating more rapidly than the mostly-stable medium of film. Not to mention
there is much more content (and #content). We are presenting on a website with
some embedded media in it.

Here's a modified version of the presentation description written by us (90%
mostly Travis):

*"Rhonda (with a heart) is an enigma of sorts. Her music CDs circulated around
college radio stations in the mid-2000s, including gems such as “Country
Breast,” “FairyTale Lost,” and “Secret Anxiety.” Rhonda’s music might be best
described as having a post-structuralist country diva twang. The origins of
Rhonda’s musical career are vague, and what little knowledge exists resides on
her webpage, of which she purports to have built herself. Describing herself as
a “freelance creative artist” Rhonda’s webpage is filled with broken links,
half-formed statements about her creative process, and a homepage that requires
you to release Rhonda from her chastity belt before entering. Mixed in with this
are a handful of her music videos for some of the aforementioned songs. These
files are buried beneath broken Adobe plug-ins and defunct MySpace video files,
which means reformulating Rhonda’s video ouvre proves quite challenging. Yet
doing so also opens up a small window into who Rhonda was, what she imagined her
music to be, and as of 2016 where Rhonda is now."*

This blog post, then, is going to act as an informal case study of [a
"homemade" y2k-era website](http://www.rhondarealeases.com) and what a light
archaelogy of the video elements can
tell us about preserving that which is partially gone and niche knowledge that
has been partially forgotten. I'm not going to dive into a lot of really
interesting and important aspects of this -- this is like a whole field of
research -- but leaning on the history of video playback on the web and the many
different video formats that are found on the site, as that is the purpose of
our presentation: trying to dig these video elements out of the aging website.
But despite this blog post already being pretty lengthy, I won't even dive
deeply into that.

If you're interested in *personally preserving* this site or stepping along with
my investigation, you can run this command to download (relatively) everything
on the site and do your own exploration:
`wget --no-parent -r http://www.rhondarealeases.com/media`

## Some general site information

As with a lot of websites, some of the content has been captured and lives on
archive.org -- you can see what was captured and when
[here](https://web.archive.org/web/*/http://www.rhondarealeases.com). This can
give us some context into approximately when the site was active.

The site was made with Yahoo SiteBuilder, which can be confirmed through looking
at the source code and in [a WHOIS search for the domain
name](https://whois.icann.org/en/lookup?name=rhondarealeases.com). The
registrar is TUCOWS, INC. ([IANA](https://www.iana.org/) ID 69, nice) and the
reseller is "Yahoo Small Business," which I suppose is still, somehow, in
business or at least maintaining business.

Here's a positive description of the service:

"Yahoo! Site Builder is a free website building application that makes it easy
to build sites and incorporate e-commerce tools into them. People who have zero
programming experience can build sites within minutes using this tool."
[source](https://yahoositebuilder.en.softonic.com/)

And here's a not-so-positive description:

"Yahoo SiteBuilder is a woefully outdated offline fossil of a website builder,
though its continued existence long past the point of irrelevancy makes it
acutely representative of the terminal malaise of its erstwhile corporate
parent."
[source](https://www.merchantmaverick.com/reviews/yahoo-sitebuilder-review/)

Okay! Enough about the site itself, let's get into the video content.

## Embedding videos

![rhonda](/images/rhonda1.jpg)

Most of the videos are meant to be played in the browser. Videos do not play, at
least not on modern browsers. Some pages have auto-play audio.

The [video on this page entitled
Cabin](http://www.rhondarealeases.com/Cabin.html), for example, says "No video
with supported format and MIME type found." but (like both videos found on [this
page](http://www.rhondarealeases.com/VideosMore.html)) are embedded on the page
and link to `pluginspage="http://www.apple.com/quicktime/download"`. The web was
a more unruly time at the turn of the century, and I think that's apparently
through the bits of the embedded objects code that read
`classid="clsid:02BF25D5-8C17-4B23-BC80-D3488ABDDC6B"
codebase="http://www.apple.com/qtactivex/qtplugin.cab"`. My guess is that when
someone clicked "Play" on the video, it would call out to Apple to download a
quicktime plugin, unpack it, run it in the browser, and that would allow the
video to play. A theory I have is that these files would then be streamed for
the rest of the content, via a proprietary playback plug-in, so loading the
first small bit of the video was all that was necessary until the rest could
buffer and be streamed.

## All videos

![rhonda](/images/rhonda2.jpg)

The video `cabin_scene.mov` is found 3 times in 4 different places in the web
structure but they are exactly the same file (this includes
`copy_of_cabin_scene.mov`). Running md5sum on all of them, the checksums match.
I think it's likely that Rhonda was uploading the file in different folders
until one of them worked with the code she had put on the webpage using the
[WYSIWYG](https://en.wikipedia.org/wiki/WYSIWYG) editor.

In total, there are 16 unique videos. This includes a video entitled
Windows_Movie_Maker_Sample_File.wmv and it is exactly what it says it is (and it
is a nightmare in and of itself) and doesn't count as original content. So, 15
videos total.

But the WMV file living on the website for no particular reason gives us a hint,
Rhonda might have been using Windows Movie Maker to edit her videos, if they
were edited and didn't come straight from the camera (like 3 of the MOV files).
This also would mean she is working from a Windows computer. Windows Movie Maker
came installed starting on Windows ME (personal note: my most hated operating
system of all time) and subsequent Windows Vista. It was discontinued [just
last
year](https://support.microsoft.com/en-us/help/4054502/windows-10-movie-maker-is-no-longer-available-for-download).
This isn't revealed in any of the technical metadata within the videos, though,
and there's some indication that Apple's Quicktime was involved instead of
Windows Media Maker, but still a use of Apple Quicktime by way of Microsoft
products. Yahoo! Sitebuilder was also a product available probably-exclusively
on Windows.

Out of the 15 videos featuring original content...
* 10 are MOV (4 kinds)
* 4 are AVI (2 kinds)
* 1 is MPG

And out of all of these videos, none are [compatible with modern web
playback](https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats)
(natively, with the `<video>` tag). This tag wasn't even around when this site
was being built (it was being developed around the time, in the late 2000s), so
that's not surprising. Video on the web underwent some really massive
transitions in the past decade, especially when this site was active.

## Formats

Just because ten out of fifteen of the videos are MOV at a glance (via file
extension), it doesn't mean they are all the same. Here's a breakdown
(statistics derived using [MediaInfo](https://mediaarea.net/en/MediaInfo)):

**How_Can_We_Stay_Mad.mov, eggwashqt.mov, imtoosexy.mov,
videohow_can_we_stay_mad03.mov, and autobio2005.mov**

* Container: Quicktime
* Video codec: Sorenson Media Video 3 (Apple QuickTime 5)
* Audio codec: PCM

**My_House_Got_Egged.mov**

* Container: MPEG-4
* Video codec: Sorenson Media Video 3 (Apple QuickTime 5)
* Audio codec: PCM

Something is up with **My_House_Got_Egged.mov**. It uses the same codecs as the
others but claims to have a MPEG-4 container. Mediainfo notes a `Format profile`
of Quicktime. This denotes that Quicktime (the software library) was used to do
the encoding here. It's interesting that this one is different from the above
videos, but it could be that this one was edited while the other were just cut
clips.

**cabin_scene.mov, grammy2.mov, and party_lady_020.mov**

* Quicktime (`EASTMAN KODAK COMPANY  KODAK DX4530 ZOOM DIGITAL CAMERA`)
* Video codec: h263
* Audio codec: ADPCM (U-Law)

I am thinking these videos were moved straight from the above digital camera,
renamed, and embedded into the site using the sitebuilder's drag-and-drop
feature. h263 is a codec optimized for compression over quality, good for files
in transit. ADPCM is short for "Adaptive
differential pulse-code modulation."

There is an additional .mov, **Intercepted_Kiss.mov**, and it doesn't hold any
decipherable data. Dramatic! I didn't spend a lot of time on this, but a hexdump
shows that most of the rows of data are just empty, and there's a tiny bit of
data at the end of the file. This data doesn't seem to include any [magic
numbers](https://en.wikipedia.org/wiki/Magic_number_(programming)) or something
else that would make it decipherable as another filetype.

Next, there are three files wrapped in Microsoft's AVI container, and their codecs are all consistent with each other.

**My_House_Got_Egged_finale.avi, Wilma.avi, MVI_0370.AVI, jumpinhole.AVI**

* Container: AVI
* Video codec: Indeo 4 Intel Indeo Video 5.0 Wavelet
* Audio codec: PCM

 The Indeo codec was developed for "real-time video playback on desktop CPUs" in the 1990s. This [seems like](https://www.siggraph.org/education/materials/HyperGraph/video/codecs/IVI.html) it was rolled into QuickTime 3 for Windows, another clue as to the source environment with which these videos were created and the site was developed.

And there is one MPG.

**rowdy_mpg.mpg**

* Container: MPEG-PS
* Video codec: MPEG Video
* Audio codec: MPEG Audio

This MPG file is super small (<2MB) and playback is a still frame and very small
clip of audio, and then no other playback. The estimated duration (as
understood by MediaInfo) is a little under 1.5seconds.
[FFprobe](https://www.ffmpeg.org/ffprobe.html) indicates the duration should be
10 seconds.

## Transcoding broken files

Getting all the files together is one thing, and playing them back is another.
Through VLC, some of them play back fine, some play partially, and some have a
sort of studder. A few have less than half a second of frames (audio and video)
before going completely blank, but the total duration is there, probably because
the duration is stored in the header. 

To understand what is going on with files that VLC is clever enough to patch and
keep playing, attempting to transcode them to another format helped quickly
reveal errors.

Doing this without creating an output file is possible: `ffmpeg -v error -i your-video.mov -f null -`

The following files (eight out of the fifteen!) are broken/partial and give
error messages (six different errors!):

**imtoosexy.mov and My_House_Got_Egged.mov**

* [svq3 @ 0x555b076b6340] slice after bitstream end
* Error while decoding stream #0:0: Operation not permitted

**videohow_can_we_stay_mad03.mov and autobio2005.mov**

* [pcm_s16le @ 0x559e299e8480] Invalid PCM packet, data has size 2 but at least a size of 4 was expected
* Error while decoding stream #0:1: Invalid data found when processing input
* [mov,mp4,m4a,3gp,3g2,mj2 @ 0x559e299d7380] stream 1, offset 0x35813e: partial file
* videohow_can_we_stay_mad03.mov: Invalid data found when processing input

**My_House_Got_Egged_finale.avi**

* [indeo5 @ 0x5574e36aa840] Corrupted tile data encountered!
* [indeo5 @ 0x5574e36aa840] Error while decoding band: 0, plane: 0
* Error while decoding stream #0:0: Invalid data found when processing input

**rowdy_mpg.mpg**

* [mpeg1video @ 0x557b4c17ec40] ac-tex damaged at 5 2
* [mpeg1video @ 0x557b4c17ec40] Warning MVs not available
* [mpeg1video @ 0x557b4c17ec40] Invalid mb type in B-frame at 5 8
* [mpeg1video @ 0x557b4c17ec40] Warning MVs not available
* [mpeg1video @ 0x557b4c17ec40] ac-tex damaged at 7 6
* [mpeg1video @ 0x557b4c17ec40] Warning MVs not available
* [null @ 0x557b4c16c5c0] Application provided invalid, non monotonically
  increasing dts to muxer in stream 0: 302 >= 30

**MVI_0370.AVI**
* [mjpeg @ 0x563f04c016c0] overread 7

**Intercepted_Kiss.mov**
* [mov,mp4,m4a,3gp,3g2,mj2 @ 0x561a0007c380] moov atom not found
* Intercepted_Kiss.mov: Invalid data found when processing input


What a wealth of errors! It'd be fun to dig into each and every one of these and
explain what the problem is, but this blog post is already getting a little bit long.

## Conclusion(?)

The conclusion is inconclusive. This is a light investigation. There's an
interesting tangled web of media codecs fully in play in the y2k era -- not
enough for me to unpack without spending a lot of time researching each one and
how they related to each other. I was an active internet user frequently
frustated by video formats during this era (I whine about this in [this
conference talk](https://www.youtube.com/watch?v=03PksEfy9ZQ) -- "if there was
ever a codec war, I'm sure it took place around me during this time"), but I
wasn't savvy to the actual encoding processes. But BLESS VLC (and [support
them](https://www.videolan.org/support/)) for absolutely changing the game in
playback support in the 2000s (I used VLC as well as FFplay to test playing
back these videos in 2019). Maybe an in-depth project to take on in the future?

When this site was presented to me, the assumption was that the videos were just
not available at all anymore. They don't play back in the browser, and ability
to download them isn't straightforward. But with some light digging, they can
be retrieved and played back, even if some of the data is only partially
available. I managed to grab almost fifteen minutes of video, although when
trimmed for repeats and partially-corrupted files, it comes to just under 9 minutes.

![rhonda](/images/rhonda4.jpg)

As always, please direct advice and corrections to the [Issues
page](https://github.com/ablwr/ablwr.github.io/issues) or to [me
directly](https://www.twitter.com/ablwr)!
