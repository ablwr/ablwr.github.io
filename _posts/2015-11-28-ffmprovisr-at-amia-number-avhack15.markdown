---
layout: post
title: "ffmprovisr at AMIA #AVhack15"
date: 2015-11-28 17:09:47 -0500
comments: true
categories: amia, ffmprovisr
---

For this year's hackday, I brought [ffmprovisr](https://amiaopensource.github.io/ffmprovisr) to the table. This was an app I made over a year ago that hadn't been given enough attention, primarily due to lack of time. My [fumbling pitch](http://wiki.curatecamp.org/index.php/Association_of_Moving_Image_Archivists_%26_Digital_Library_Federation_Hack_Day_2015#ffmprovsr) went something like this: "I think it'd be fun to combine and continue to build up these two projects into something better because ffmpeg continues to live on as a mysterious but necessary component of a/v archival practice. This project would be mostly R&D with some basic front-end web development skills (building forms). I feel this is a little out of the scope of hack day (and those greedy for rewards may seek refuge elsewhere) in that it's more of a REMIX project and a mostly-hack-the-docs-with-some-coding project, but if there is interest (there was last year, for ffmprovisr) -- we will build the hell outta this!"

I envisioned building on the old version of ffmprovisr, which was a guided form for building ffmpeg scripts, but on hack day I realized it was a little too heavy on the hand-holding -- archivists that at least had ffmpeg installed on their computers didn't need to click through forms and select their input and output. They could reasonably be expected to have the ability to look at a sample script and base their own script off of it. So we changed the structure from a form to a sample command line that also came with a description of what it did and a breakdown of how each command worked.

![](/images/thinkingffmprovisr.jpg)

When originally pitching this idea, I thought it'd be a good "gateway drug" to capture archivists and turn them into developers, anticipating a lot of git knowledge sharing and code-writing habits. In the end, I was primarily the one pushing code (but also Rebecca Fraimow) while everyone else helped to add interesting sample scripts to our shared google doc, parsing commands pulled from the ffmpeg documentation from previous hackdays or dropping in scripts they use regularly as archivists. So the project ended up being even stronger than I imagined it would be (and helped provide the biggest lack from the existing proof-of-concept application)!

So the best part about hackday was the collabartive elements. It was great seeing collaboration happen live between [BAVC employees](https://bavc.org/) and [Reto Kromer](http://reto.ch/), as well as get some in-use scripts from Catriona Schlosser from [CUNY-TV](http://www.cuny.tv/) and Nicole Martin from [Human Rights Watch](https://www.hrw.org/). While Eddy Colloton (MIAP) was working on a script that converts a DCP into access copies, help came in on our shared google doc from Kieren O'Leary ([Irish Film Archive](http://www.ifi.ie/archive)), participating remotely from Ireland.

![](/images/ffmprovisrtransfer.png)

We had been working on a forked branch of my original repo, but when I came home from AMIA, I did the right thing and gave ffmprovisr to the people -- it now has a permanent home in the [amiaopensource repo](https://github.com/amiaopensource/ffmprovisr) where collaboration has continued to thrive, mostly thanks to the strong support from Reto, who diligently modified the code to make it consistent and easier to read. Thanks, Reto! 

P.S. super happy I went 2009-trendy-internet-tumblr-style with the name of this app because I saw tweets go out as ffmprovisor, ffmproviser, and ffmprovisr (and maybe a few other variations in between).