---
layout: post
title: "Lenticular film, lenticular codec"
date: 2018-04-04
---

Today I explored Reto Kromer's [Lenticular codec](https://github.com/amiaopensource/lenticular) (original code written by Joakim Reuteler in 2012, adapted and added to AMIA Open Source in 2017-2018) because it is available, it is open, I know the author (always helps), it is written in C, and I know about lenticular film.

Quick crash course in lenticular film: It was a film processing format used around the early 1930s to produce simple color film (tints things green and red). It is like lenticular photos and is a cool [technical problem/solution](https://en.wikipedia.org/wiki/Lenticular_printing) all on its own.

![lenticular](/images/lenticular.jpg)

First to run `lenticular`, I had to get some files so I nabbed something I knew was lenticular from [http://mirc.sc.edu/](http://mirc.sc.edu/), which I know about because I used to work there. I used [this footage](https://mirc.sc.edu/islandora/object/usc%3A1554) from a rockin' rich lady who toured the world in the 1930s and took footage from all over the place (warning: extremely colonialist gaze, as you might would expect). She also really liked horse-racing and the Girl Scouts and her dogs and film.

I went off to figure out how to convert this video to individual images but fortunately the docs already gave the commands I needed to run to convert to the supported greyscale tif.

Then I had some issues getting the code to work, but requested [a sample command](https://github.com/amiaopensource/lenticular/issues/2) and received it. Mostly I had a lot of "user error" to sort out.

Emailed the maintainer (since he is a friend) and got:  

"You can of course digitally create your own by reversing the  
algorithm, but this would not give you real-world files. In my  
personal opinion, this would not be really of interest."  

Interest piqued here. I think this is OF GREAT INTEREST.  

Still, working on running lenticular correctly, getting `Segmentation Fault 11` often. I might come back to understanding errors in C later, in fact I'm pretty sure I will, but I'm moving forward for now. I think my computer was just running out of available RAM and the tool is just overexerting itself. I was able to get quite a bit through fits-and-starts but processing this many .tif files in rapid succession is just not going to work out for me. That's okay though.

I basically took many medium-sized black-and-white images and converted it into a tiny-sized images with some wavy color.

I then converted it to a video and, for purposes of sharing, a very tiny little gif:

![tiny lenticular](/images/tiny-lenticular1.gif)  

(It's horse-racing. The footage isn't that clear even when at maximum quality, like above.)  

Tried to generate something more high-rez out of the low-rez but archival .tif files are very very big and I filled up my already-limited disk space with 40GB of images for only a few seconds of footage before my computer gave up. Bye, files!

Onward! To the Internet Archive! Found this home movie from Hawaii generously uploaded by AV_Geeks and made open by UPenn: [Hawaii](https://archive.org/details/upenn-f16-0522_Hawaii)!

This took a long time to download, so I spent some time thinking about everyone uploading their backups to a cheap cloud storage solution and how long it would take for them to get it all back down again.

I did the process again and got a little bit out of the larger file, mostly by repeating the task over and over, manually.

![tiny lenticular](/images/tiny-lenticular.gif)

Tada! Two teeny-tiny lenticulars! 

These would look a lot nicer if I had access to very large files and my computer could handle processing them, but it's good to be able to see and think through how all of the inner workings of data manipuulation works. Thanks Reto for working on this codec prototype (very early in development) and making it open for me to use and learn from. And now that I got it working, I can finally dig into the code!
