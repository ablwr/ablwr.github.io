---
layout: post
title: "How to livestream and record a conference when you have no money"
date: 2017-05-13
tags: [conferences, teaching, video, livestream]
---

I've explained this to so many people and thought about this so much that I had to check and make sure I definitely have not written about this on my blog before, but it turns out that I have not.

### First, what is this going to be about?

This is a guide to setting up a lo-fi but totally acceptable livestreaming and conference video recording situation using affordable equipment, much of which can be found or borrowed.

If you can afford a service like [Confreaks](http://www.confreaks.com/), I really recommend it! They are very nice people and do great work. However, this guide is for when you are in a low-budget situation and it's better to do it yourself than not do it at all. No excuses!

### What do I need?

Hardware:
- *A camera*

   Any old handheld camcorder that can plug into a computer will work. Two is even better (one for the speaker, one for the slides)!
- *A tripod*

   Tripods go a long way in producing stable video streams. You don't want to try to set up a camera without one.
- *An analog-to-digital converter*

   I recommend BlackMagic brand because they use an open source SDK. [This](https://smile.amazon.com/gp/product/B009D91314/ref=s9_dcacsd_dcoop_bw_c_x_1_w) is the cheapest option. [This one](https://smile.amazon.com/Blackmagic-Design-Intensity-Shuttle-Thunderbolt/dp/B007ZDHDRS/) is fine. [This one](https://smile.amazon.com/Blackmagic-Design-Express-UltraStudio/dp/B008RTY2XC) is the best, if you are looking for an excuse to buy one for digitization anyway -- it's worth the extra $. I've used the latter two successfully but I've seen the first in action.
- *A computer*

   An average laptop is fine. The above converters are Thunderbolt, so make sure to buy a USB3 one if your computer only has USB3.
- *Cables!*

   You'll need cables to connect the camera to the converter, converter to the computer. Audio from source to the converter (if possible). I don't know what cables you will need, but [The Cable Bible](https://amiaopensource.github.io/cable-bible/) might be a valuable resource to you.

- *Optional: external harddrive*

Software:
- [Open Broadcaster Software](https://obsproject.com/) or [Wirecast](http://www.telestream.net/wirecastplay/landing.htm)
- A YouTube account

### What do I do?

Try to get into your venue a day in advance to setup and run a test trial. It's very stressful to try to do this right before the conference is about to start, and if you are reading this, there's a large chance that you are also organizing the conference and are already very stressed.

First, set up the video camera on the tripod, connect it to the analog-to-digital converter, and connect the converter to the computer. You'll probably have to install the BlackMagic drivers so the computer knows what is being plugged into it (this is familiar to Linux users or people who used computers in the 20th century and less familiar to those who haven't -- installing drivers!). Install one of the above software (OBS or Wirecast) and run it, and it should help you through the process. This is where you will set up the ability to record the footage to your harddrive (Warning: You may need an external harddrive to store footage, as it takes up a lot of space).

If you are lucky, everything will work and you'll see a video stream on your computer eager to be recorded. If you are less lucky, you might spend a few hours debugging and trying to get the video to appear on the screen by changing various settings.  Good luck to you.

Next, you'll need to plug into the sound system that amplifies the speaker's voice to the conference room. The cables you will need will depend on that setup, and you might need some extensions to run the cable from the front to the back of the room, if necessary. Plug a cable from the sound system into the analog-to-digital converter and you should hear it broadcasting in the software. If the conference room is very small, you might be able to get away with using the camera's audio (but it will not be great, so only do this as a last resort).

Adjust the settings in the recording software so video is coming from the camera and audio is coming from the sound system.

With this setup, someone will have to monitor the camera and toggle between the speaker and their slides while streaming. If you are just recording and planning to edit the videos later, you can keep the camera on the person speaking and collect slide decks and edit them together in post-production. A second camera can be added to the setup to just record the screen and toggling between the two can happen within the software.

Okay, next, head over to YouTube and their [Live Dashboard](https://www.youtube.com/live_dashboard). This is where you configure YouTube to start streaming when the conference is ready. Make sure to test out a livestream before the conference starts so you are comfortable with all of the settings, how to turn the stream on-and-off, and mostly ensure that it works.

And that's it! The hardest part is the setup! When recording, make sure there are two people monitoring the stream and swap out volunteers, so no one gets too tired and grumpy. Watching a stream and also monitoring many levels of social media for people complaining about the service you're providing for free can be very exhausting.

** Bonus note! Do NOT stream any audio under copyright over YouTube or they will take your video offline. It sucks but that's how it goes, even if you do it accidentally and only for a minute (this happened to us at Code4lib2016). It's the tradeoff for using YouTube. If your conference is playing fun music during the breaks, just make sure to mute or pause the livestream during this time.

### Wait, why should I listen to you?

I have a whole bunch of years of experience working with video in a preservation setting and little bit in a production setting. I have set up and run livestreaming for [Code4lib](https://code4lib.org/) and [No Time To Wait](https://github.com/preforma/notimetowait), and have given this advice to those intending to livestream several conferences (with full success). I also know that this is the setup used by conference videostreaming experts. So if you don't trust me, trust them (via me)!

### External Resources

The planning/resources list from Cod4lib 2016 is available [here](https://wiki.code4lib.org/2016_Video_Recording_%26_Streaming).

The resources list from No Time To Wait! is listed at the bottom of this [README](https://github.com/preforma/notimetowait#streaming).
