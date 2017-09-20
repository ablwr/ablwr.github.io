---
layout: post
title: "How do web archiving frameworks work?"
date: 2017-09-20
---

<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span> ![pc](/images/computer_e-mail.gif)   

*"If you wish to make apple pie from scratch, you must first create the universe."*

If you wish to explain how web archiving works from a technical standpoint, you must first understand the ecosystem. I was anticipating writing a blog post about website archivability from a development perspective ("How can I make my website more archivable?") but realized I needed to provide an overview of web archiving in general (even if just for my own comprehension). I don't feel like this information is especially clear and available on the web -- but if I am just missing out on a solid resource, [let me know](https://twitter.com/ablwr). Likewise, if I'm wrong about something (which I probably am), let me know. BIG THANKS to [Karl-Rainer Blumenthal](http://landscapelibrarian.com/) for speaking at the Joint Meeting of New York City & Mid-Atlantic Archive-It partner groups at [METRO](http://metro.org/) last week, which gave me the inspo, and for clarifying my questions on the above information (and correcting my incorrect assumptions).

## OK COMPUTER

<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span> ![pc](/images/computer_e-mail.gif)  

Some champion frameworks (not counting top-dawg [Wayback Machine](archive.org/web)) in the web-archiving ecosystem funnel are [Archive-It](https://archive-it.org/) and [Webrecorder](https://webrecorder.io/). There are other methods (good ol' [wget](https://www.gnu.org/software/wget/), e.g.), but these get a lot of hype. And I feel like they are frequently pitted against each other, even though they serve different purposes, so they shouldn't be thought of in this way. Archive-It and Webrecorder are platforms that allow people to easily use the underlying web archiving technology. When unhappy with one or the other, it's probably mostly comments on the provided design experience rather than the backend frameworks.

Archive-It is built for institutional-level integration and scale. On top of archiving, it is able to perform scheduling and also exists as a hosting service that stores this data for institutions. Webrecorder can do this too, but isn't built with this in mind as a business model. It expects the users to manage their own digital preservation storage, although you can still save and share "recorded" websites. Webrecorder's tagline is "Web Archiving For All!" -- it really does democratize and make-more-open what Internet Archive has been doing, which makes me like it a lot. But they are different!

## So, technically...

<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span> ![pc](/images/computer_e-mail.gif)  

This section should really emphasize the power of open source tools. Are you ready?

First! All these tools produce the same output, the [WARC](https://www.loc.gov/preservation/digital/formats/fdd/fdd000236.shtml) (Web ARChive) file format. Standards are great. This is ostensibly an [open format](https://en.wikipedia.org/wiki/Open_format), although unfortunately standardized through ISO, so it's not free to view. (But that is a personal digression...) The [IIPC](http://netpreserve.org/) (International Internet Preservation Consortium) has put together an open [warc-specifications](http://iipc.github.io/warc-specifications/) page for more information about this, specifically [here](http://iipc.github.io/warc-specifications/specifications/warc-format/warc-1.0/), which seems to be very close to what is probably in the official ISO that costs a hundred bucks. Anyway, WARC is essentially a wrapper for web-related materials, and it aggregates that information along with relevant metadata for future context. Like a zip file, but specifically made for websites.

Second! Here things get more complicated.

**Internet Archive**'s [Wayback Machine](archive.org/web) is built on [Heritrix](https://github.com/internetarchive/heritrix3) (heritrix3), web-crawling software. Heritrix is built in Java. It does the heavy work of turning websites into web archives. The Wayback Machine used to use a Java-based framework for "replaying" archived websites, but it was re-written in Python, so now it uses that. It also depends on [umbra](https://github.com/internetarchive/umbra) a queue-based browser automation tool, to grab up those sites and dependencies.

**Archive-It**'s stack looks like the Wayback Machine, for the most part. However! Archive-It is transitioning to using [brozzler](https://github.com/internetarchive/brozzler) and [warcprox](https://github.com/internetarchive/warcprox). Brozzler is built on top of [Chromium](https://www.chromium.org/Home), among other things, and is able to view websites. warcprox is built on [pymiproxy](https://github.com/allfro/pymiproxy) and helps with turning the websites into WARC files. Combined, and built on the tools below, they are able to do the work of grabbing (brozzler) and saving (warcprox) websites. For audiovisual material, it uses [youtube-dl](https://github.com/rg3/youtube-dl/), an open source tool for downloading media (and not just for YouTube, despite the name).

**Webrecorder**, on the other hand, depends on [pywb](https://github.com/ikreymer/pywb), a Python implementation of the Wayback Machine, for both the "capturing" of live sites and "replaying" of the generated web archives. Webrecorder is then developed on top of pywb (conveniently both primary created by web archiving developer *superstar* [Ilya Kreymer](https://github.com/ikreymer)!)

**Nota bene** Open source is great! We can do so many great things because people have shared their code and collaborated together, and have been able to build things on top of other things.  

<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span>
<span style="float:left;">
![pc](/images/computer_e-mail.gif)
</span> ![pc](/images/computer_e-mail.gif)  

## More!

For more web archiving resources, see...  

- IIPC's [awesome-web-archiving list](https://github.com/iipc/awesome-web-archiving).  
- IIPC's [OpenWayback](https://github.com/iipc/openwayback/wiki).
- [WAIL](https://machawk1.github.io/wail/), a "GUI atop multiple web archiving tools intended to be used as an easy way for anyone to preserve and replay web pages."
OK, stay tuned while I put together the blog post I originally intended to write, about web accessibility and website archivability, in which I argue with myself about both.
