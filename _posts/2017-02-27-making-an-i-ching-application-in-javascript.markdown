---
layout: post
title: "Making an I Ching application in Javascript"
date: 2017-02-27
tags: [small projects]
---
This is the process I used to go about building a small, for-fun webpage. I hope this can help demystify the process of building a website, even if just a little bit.

![](/images/hexagrams.gif)

My first step was the figure out how the I Ching worked, which means going to Wikipedia and reading about it. This scared me a little bit, because the [process is pretty complicated](https://en.wikipedia.org/wiki/I_Ching_divination). You know, it's like the O.G. algorithm. There's an algorithm used in cryptography (and used in macOS's /dev/random) named after one of the I Ching divination methods, [the Yarrow algorithm](https://en.wikipedia.org/wiki/Yarrow_algorithm). Well, that's enough "research" because now I know what I need to know -- I either need to build one of these divination algorithms, find one, or pretend to.

Then I went to [existing I Ching sites](http://www.ichingonline.net/) to see how they were built -- they all seem to be built in PHP and therefore run in an obfuscated way (so I couldn't rip them off).

I found the [I-Ching App of Changes](http://www.brian-fitzgerald.net/i-ching/) and the snippet of open source code that constructed the "yarrow method" of I Ching hexagram construction. What a lifesaver! A lifesaver with an MIT license on it! Now I can be confident that my website will be using the best of the best for oracle-consulting.

Taking a break from the parts that might involve math, I set up some JSON by doing some copy-pasting trickery from Wikipedia and multi-cursor pasting in a rad text editor (I am currently using Atom). Computers are amazing and it only took a few clicks instead of a painful copy-paste for each part of the 64 hexagrams. That's 64x3! I added a definition, the symbol that represents each hex (cool to find although [not reliable](https://twitter.com/beet_keeper/status/836697584148201472)), and the number (so I can link to other websites that base results on the hexagram number).

The hard problem was the algorithm and that was solved. The easy problem was how to apply the algorithm and produce a cast hexagram and a transformed hexagram based on six clicks (by throwing yarrow six times and counting, or using three coins, etc). Looking at the open source yarrow-sorting code, I came up with a plan to have `1` represent an unbroken and unchanging line, `0` to represent a broken and unchanging line, `x` to represent an unbroken line changing to broken (strong to weak), and `o` to represent a broken line changing to unbroken (weak to strong).

Each click of the button does this sort and applies the results (one of the four options) to a string, resulting in a string that can be "decoded" into the first, cast hexagram, and second, transformed hexagram, by switching the `x` and `o`s out for what they were and what they would become. This was initially hard to wrap my head around, but once I understood it, it was very easy to implement in Javascript so each hexagram could be displayed by pulling the codes out of the hexagrams.json file.

(I also didn't feel like standing up a server for testing this, and the json file isn't very big, so I actually faked it and made a faux hash inside of a variable. Whatever works.)

But, for example, if the yarrow algorithm throws "11xxo1" as the result, that would turn into 110011 (which is the hexagram 61, Centre Conforming) and change to 111101 (which is the hexagram 14, Great Possessing)

Now that the meat of the application was done, I could set up the DOM. I thought about using [React](https://facebook.github.io/react/) until I realized it didn't make sense to use a framework with a million dependencies just to render a little bit of content, and I used tried-and-true good-old-friend [jQuery](http://jquery.com/). I'm old and not that hip, so my code is, too.

![](/images/iching.png)

With the DOM set up, I could now dress it up. This used to be my least favorite part because I would get so frustrated with CSS that I would want to scream, but now I don't feel that way anymore.

I wanted mood ring vibes. To do this, I went to Codepen, searched for color changing background, and cruised until I found something that fit what I wanted. Then I copy-pasted that sucker and made adjustments until it looked right and had the right tones. If copy-pasting code from the internet is wrong, I don't ever ever wanna be right (nor have I ever ever been right). This made the page look extravagant and beautiful and mature but it took very little work.

In more practical matters, [Skeleton](http://getskeleton.com/) has been my not-Bootstrap framework of choice. [Google Fonts](https://fonts.google.com/specimen/Ruthie) hooked me up with some additional fancy.

That's that. That's how a single-page simple webpage works! This only took me a couple of hours, but two years ago it may have taken me all day! Sometimes it's hard to tell you are learning anything when you are always learning, so this was a good exercise to go back and try something small to realize that you have learned at all. [My code is online](https://github.com/ablwr/i-ching), as usual, if you want to use it as a reference and learn how to make your own divinations.
