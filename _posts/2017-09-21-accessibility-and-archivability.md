---
layout: post
title: "Accessibility and Archivability"
date: 2017-09-20
---

Okay, so this is the follow-up post to [this](https://ablwr.github.io/blog/2017/09/20/how-do-web-archiving-frameworks-work/) (or, rather, that was the aperitif post to this one). I was at the Joint Meeting of New York City & Mid-Atlantic Archive-It partner groups at [METRO](http://metro.org/) a little while ago, and a question came up about how to best guide creators towards good practices in the website development stage, to better support future preservation efforts. There are some guides in place for this (jump to the bottom of this page for additional resources). But, like, I'm a developer. I threw out the idea that a good guideline to use was that if a website is *accessible*, it should also be *archivable*, that these guidelines can go hand-in-hand. And people building websites should already be concerned with accessibility and aware of related best practices (and if not, they are bad at their jobs and you should replace them with good people). That sounds good, but am I right? Am I wrong? I decided to make sure I wasn't totally full of shit, and here are the results.

The point of this post is to be able to communicate better with people who *build* websites, so their websites are more likely to be archivable in the future. (And I'm intentionally holding myself back from using technical jargon here.)

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

## What does it mean for a site to be *accessible*?

There are plenty of great resources to explain the basics, but fundamentally a website should be able to be accessed and understood by anybody, regardless of their level of ability. [WebAIM](http://webaim.org/intro/) summarizes the four major categories as **visual, hearing, motor, and cognitive**. Some quick ways to assess a site without any additional programs are:

- Does the structure of the website look OK and make semantic sense?
- Can you use your website using only your keyboard?
- Can you size up to 200% and your site won't break?

There are SO MANY other things to consider. That's just the tip-top level for testing without installing tools for that purpose or having knowledge about how websites are built.

## What does it mean for a site to be *archiveable*?

Obviously there's a lot less written on this, but a website should be able to be saved as a WARC file by some sort of web archiving process (like [Wayback Machine](http://archive.org/web/) or [Webrecorder](https://webrecorder.io/)) and look&function the same as it did when it was "live." Can everything be "played back" in the future just as well as when it was captured for posterity?

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

## And how do these work together (or do they)?

Web crawlers are little robots that save your things and play them back again. Thanks, lil dudes. And one of the core principles of accessibility practice is a website's ability to work using assistive technology (like screen readers), and those are also like little robots that read things. For accessibility in general, the content of the webpage should always be clear regardless of the way in which it is being accessed. It makes sense that if one works well, the other should work well too.

Below are a few examples that hopefully highlight how care towards accessibility helps archivability.  

**Example 1: Internet Girlfriend Club / Asynchronous loading**  

[This site](http://internetgirlfriend.club/) was loading CSS asynchronously, after everything else had loaded on the page, and it used JavaScript to do that. I don't really know why, I guess that has a usecase somewhere, but it wasn't necessary here. CSS is not necessary for accessibility here (but not to say that it [isn't important](https://medium.com/@matuzo/writing-css-with-accessibility-in-mind-8514a0007939)) -- IGC passes these tests -- but if something more significant was loading up in a delayed way with JavaScript, like links, it wouldn't know how to save them because the Wayback Machine is taking things at initial-load face value. Webrecorder doesn't have this problem, although the problem was evident by the flash of white before each page would load. Bonus note: this pattern is known as Flash of Unstyled Content (FOUC)! Fortunately, this is my website (meta-hyping here), so I was able to [fix it right away](https://twitter.com/ablwr/status/909952495664984064). Archive yer heart out! JavaScript doesn't have to be avoided, but it should be used carefully and correctly (and not flippantly, which I was guilty of!)

**Example 2: Karlie Kloss / Wix**  

Karlie Kloss's [site](https://www.karliekloss.com/) is built in Wix, which is not very good for accessibility *or* archivability (this seems to be the general consensus). Accessibility-wise, trying to use this site without a mouse is impossible -- it highlights something, but what is being highlighted is unclear. Fumbling, I accidentally opened a link I couldn't see (because tabbing took me to the bottom of the page -- what?), and it was [this article about learning how to code](https://www.fastcompany.com/3066342/how-model-karlie-kloss-followed-her-nerdy-passions-to-found-kode-with-klossy). I found it in an auto-rotating carousel, above a gif. And the top nav, which is only a lil "hamburger" (the [widely-hated hamburger menu](https://www.google.com/search?q=stop+using+the+hamburger+menu&oq=stop+using+the+hamburger+menu)), is unclear. This website is all-around bogus for a lot of other reasons and I hope Karlie calls me to fix it.

The latest version of her site shows [nothing](http://web.archive.org/web/20170915110314/https://www.karliekloss.com/) in the Wayback Machine and acts weird when [making an attempt in Webrecorder](https://webrecorder.io/ablwr/accessibility-archivability/20170919170152$br:chrome:53/https://www.karliekloss.com/), so I don't have a lot of faith in its archivability. Karlie is just not going to make it into the archive.

![awkward karlie](/images/awk-kloss.png)

**Example 3: Larry Polansky / Clear navigation**

[Lorena](https://twitter.com/dalelore) sent me [this webpage](http://aum.dartmouth.edu/~larry/) as an example of a site that looks simple, but was difficult for her to archive. Not necessarily for technical reasons, but "it's a rabbit hole of confusion because there is no site map and you can't tell if you captured all the pages cause you don't know what there is."

Likewise, this site looks totally accessible, right? No carousel, no models, no Flash... but it's very important to remember the website's structure when designing/developing for accessibility and archivability. I actually laughed out loud when I looked at the HTML:

![small.. small.. small](/images/small-small-small.png)

WHAAATTTT?? Hahaha. Imagining trying to get to the link on this page without being able to click on it. A screen reader might have to go through small ... small .. small .. small .. until it gets to the content, and even then it is confusing.

Okay, this is a contrived example because I thiiiink a screen reader will skip past these tags because it can identify them as insignificant as it relates to the content, but this is just an example of a messy, confusing site structure. This is a good time to mention that [ARIA tags](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA) should be present on websites for navigational support and those are not present, either.

Clear navigation for the entire website is crucial to archiving, and clear navigation on each page is crucial to accessibility.

## Et cetera

That's all for now, thank you! I know it's not that much and I am missing a LOT of granularity. I didn't even talk about Flash and other kinds of JavaScript, well-known enemies to both of these concepts. Even though Webrecorder now makes a lot of this possible, it doesn't mean it is preferable. (Also I wasn't willing to install Flash on my computer to test it out. 😘 ) So much more work can be done here (and I'd like to see that), with more research and better examples, but I am just one little human with a finite amount of time to spend on this!

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

## Resources, Accessibility

- [Creating an Accessibility Engineering Practice](http://blog.danielna.com/2017/09/14/creating-an-accessibility-engineering-practice.html)
- [WebAIM](http://webaim.org/) and [WAVE](http://wave.webaim.org/)
- [Easy Accessibility Testing with aXe](https://www.deque.com/products/axe/)

## Resources, Archivability

- [Stanford Libraries on Archivability](https://library.stanford.edu/projects/web-archiving/archivability)
- [Archiving the Web: A Case Study from the University of Victoria](http://web.archive.org/web/20141113023031/journal.code4lib.org/articles/10015)

Thank you again [Karl](http://landscapelibrarian.com/). Thanks to [Samantha Abrams](https://twitter.com/sabramse) and [Lorena Ramirez-Lopez](https://twitter.com/dalelore) for sample links. I learned a lot about web accessibility in my previous role at the New York Public Library when I worked with [Willa Armstrong](https://twitter.com/willaarms), an expert in this area of digital ideation. Willa is the best!
