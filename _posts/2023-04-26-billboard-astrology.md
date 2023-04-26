---
layout: post
title: "Billboard Astrology"
date: 2023-04-26 09:00:00 -0500
tags: [divination, small projects, webdev]
---

![Billboard Astrology screenshot with the base date of jan 1 2000](/images/billboard-astrology.jpg)

I made yet another "techno-divination" website! webpage? web "app"? SPA? What are we calling cute lil simple spots on the web these days?

Anyway, hello to [BILLBOARD ASTROLOGY](https://bits.ashleyblewer.com/billboard-astrology/), the 5th techno-divination.

You can see the others [here](https://ashleyblewer.com/art.html). They include the i-ching, the aura reader, the aura reader with partner, barthes tarot, and a planet-mapper.

I started on this project by looking at [this library](https://github.com/guoguo12/billboard-charts), but I didn't want to use Python for a basic website. I moved to [this billboard-top-100 npm package](https://www.npmjs.com/package/billboard-top-100), but it proved to be frustrating to use.

I looked at [enhance.dev](enhance.dev), which I do want to use in a project one day, but I wasn't able to get a node package to play nice on the web, on the client side. Which makes sense, but it is annoying. I wasted too much time on this.

After getting fed up with the state of JavaScript in 2023, something I'm always fed up with, I looked for alternative ways to do what I wanted to do with little effort (or requiring either a backend or for me to build my own billboard webscraper). 
(See also: Julia Evans' [Writing JavaScript without a build system](https://jvns.ca/blog/2023/02/16/writing-javascript-without-a-build-system/)). I feel like I was really psyched on the idea of webscraping 10 years ago, and now I'm shuddering at the thought of grappling with billboard dot com's changing HTML landscape. And that seems like something so janky, almost as janky as the state of building, installing, and maintaining JS web frameworks for a small idea.

But FORTUNATELY, I came across [this dataset](https://www.kaggle.com/datasets/dhruvildave/billboard-the-hot-100-songs) on kaggle (a site I otherwise hadn't heard of).

That was great! One drawback is that I'm not getting live data. But on the other hand, I'm not querying for live data in a spot where it's likely to change in a bad way, and charts are historical data. So why not use the data as-is instead of trying to fetch and load? I love keeping it simple.

I was able to shrink down the dataset from 18+MB to 148k by picking out only the #1 songs, keeping only the date, the artist name, and the song name. I was lazy so I managed to do this in Google Sheets, which is computationally impressive (by people who are not me) because it was a lot of lines of CSV.

After wasting a bunch of time with JS frameworks (mostly because I will go through incredible lengths to keep something as simple as possible for present-me and future-me), I was able to put this idea together in a super short amount of time, with most of the time spending on figuring out styling (because the state of CSS in 2023 is _impeccable beautiful perfect wonderful incredible_!!!).

Something I haven't done is add in error handling for dates that are too old or too young to have Billboard charting (the dataset ended at 2021, and I didn't realize I knew so many people that have recently created new humans). Something I want to note is that I did restrict the date range in HTML, so the datepicker shouldn't allow newer or older dates, but nothing will stop parents from getting more insight into their children!

Give [it a try yourself](https://bits.ashleyblewer.com/billboard-astrology/) or see what other people are getting [c/o this Mastodon post](https://digipres.club/@ashley/110259863086150970)!

![Billboard Astrology screenshot depicting taylor swifts birthday](/images/billboard-astrology2.jpg)