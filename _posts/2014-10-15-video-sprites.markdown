---
layout: post
title: "Video Sprites"
date: 2014-10-15 15:16:15 -0400
comments: true
categories: [oss, amia, video sprites]
---


Last week, I participated in the second [AMIA AV Hack Day](http://wiki.curatecamp.org/index.php?title=Association_of_Moving_Image_Archivists_%26_Digital_Library_Federation_Hack_Day_2014) and paired up with NCSU libriarian/developer Jason Ronallo, CNN archivist/engineer Nicholas Zoss, and CNN archivist/engineer/manager Jay Brown. Building on Ronallo's [work with WebVTT and video scrolling thumbnails](http://ronallo.com/blog/a-plugin-for-mediaelement-js-for-preview-thumbnails-on-hover-over-the-time-rail/), we created a Ruby gem that exports thumbnail images, thumbnail sprite image, and a WebVTT metadata file with synced media fragment URLs to thumbnails within the sprite. This could allow for the integration of video thumbnail creation to happen automatically within the web access video workflow. It is also easy to install and use, making it accessible to a wider audience (always a primary goal of mine).

One of the things I am most proud of is how seamlessly our team was able to distribute work and pair together when necessary. I was able to jump right in as the junior developer role, helping as support and Ruby syntax consultant, as well as filling out documentation and other smaller tasks. Jason Ronallo steered the ship, but welcomed many proofreading eyes to look over his code for debugging. Nick Zoss contributed plenty of engineering knowledge and helped do "all the math parts." Jay Brown went to work finding and creating sample videos for testing the scripts and worked on general QA. And at the crucial end point of the day, I wrangled Dave Rice to quickly act as ffmpeg script consultant (a cool trick I learned and helped my team win one of the awards from [the first AV Hack Day](http://wiki.curatecamp.org/index.php?title=Association_of_Moving_Image_Archivists_%26_Digital_Library_Federation_Hack_Day_2013)).

Anyway, let's get down to it! This is how the app works. It's EASY! After you `gem install video-sprites`, you can run it in your terminal (assuming you have ffmpeg and ImageMagick installed and working)

For example, I ran this: `video-sprites -i /Users/ashley/Development/kiss_from_a_rose.mpg -o /Users/ashley/Development`

And I got this:

![](/images/rose_export.png)

Simple, right? And check it out...

```
00:00:00.000 --> 00:00:05.000
http://example.com/kiss_from_a_rose-sprite-00001.jpg#xywh=0,0,200,133

00:00:05.000 --> 00:00:10.000
http://example.com/kiss_from_a_rose-sprite-00001.jpg#xywh=200,0,200,133

00:00:10.000 --> 00:00:15.000
http://example.com/kiss_from_a_rose-sprite-00001.jpg#xywh=400,0,200,133
```

There's also this WebVTT file! If I replace the example.com with the website that is hosting the image sprite (or had I specified it when I ran the gem using the -u or --url flag), I could integrate it into a scrolling video thumbnail feature! 



Play around with it yourself! The [code is up on Github](https://github.com/jronallo/video-sprites) and we welcome feedback. Moving forward, there's a lot to do to keep this gem in tip-top shape and there are many features we plan to add. Like a good junior developer, I've given myself the goal of writing tests to make it a healthy and happy gem. Oh, tests...
