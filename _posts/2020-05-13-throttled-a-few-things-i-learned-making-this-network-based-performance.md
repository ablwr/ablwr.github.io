---
layout: post
title: "Throttled: a few things I learned making this network-based performance"
date: 2020-05-13 09:00:00 -0500
tags: [programming, personal, recurse center, small projects, webdev, web preservation]
---

For the past little while, I've been working on this [network-based performance project](https://ashleyblewer.com/throttled.html) that I have named Throttled. It's a performance by 233 gifs and a very slow network connection. This blog post is a bit about what I learned while making it. I'm writing this somewhat in haste, so the notes are a bit sloppy.

This project had me asking some questions that are the opposite of what people usually want to learn about when working on projects involving website, such as:

* "slow down website"
* "load files synchronously"
* "make gif bigger"

But first, here's what I learned about each of the core components of this piece.

## The building (network)

I felt like I didn't know anything about the network server layer -- Apache server, nginx, `tc`, but I ended up knowing more than I thought I did going into this project.

My first attempt was to use my favorite web service provider, [nearlyfreespeech.net](https://nearlyfreespeech.net), but this service uses shared computing and there wasn't a way to have the control I needed in a server. Although I certainly spent a lot of time trying to get a custom .htaccess file at my server root to work -- there was not an ability to customize Apache Server modules.

I ended up asking a question on their members message board, and I got a super-quick response explaining that yeah, this module is not available, and also allowing a server to be intentionally slow would make it more susceptible to DDOS attacks, as one method is to try to lock up connections with super-slow downloads. I had never thought about that nor have had to think about that, as most of my career has been spent working on internal systems for cultural heritage institutions that are protected in other ways and in general are not user-facing.

So I had to upgrade, and I went with Digital Ocean's smallest Droplet. This way, I had control over the Apache Server and could use the [ratelimit module](https://httpd.apache.org/docs/2.4/mod/mod_ratelimit.html).

Adding this was all I needed to cap transfer speeds per network connection at a teeny-tiny rate of 1kb/s. 

```
<IfModule mod_ratelimit.c>
    <Location /images>
        SetOutputFilter RATE_LIMIT
        SetEnv rate-limit 1
    </Location>
</IfModule>
```
The lowest rate possible ended up being perfect for me.

Reading through the documentation, I also saw the [dialup module](http://httpd.apache.org/docs/2.4/mod/mod_dialup.html), which seems aligned with this project conceptually but I ended up not using it because I was wary of the control I would have, and I wanted things to be consistently very very slow. BUT I learned that that exists.

When I started this project, I was going to throttle the network using the `tc` library in the Linux kernel (TC for Traffic Control), which I just learned about and seems cool and powerful, but I ended up not doing that, just working at the network server level.

Another thing I considered when I was living in a shared computing server mentality was hosting a node server and throttling the loading that way (and I imagine I'd have even more control over making sure the images load in order). I didn't want to do this, and fortunately I didn't have to. I guess I feel like I picked the Goldilocks level of network control. I could have gone lower (Linux kernel) or higher (programming language server) but I feel happy in the middle (apache webserver).

It will be fun to play around with `tc` sometime in the future though.

Something I had zero problems with was DNS! I know, a small miracle! I'll take it.

## The stage (layout)

I feel so blessed to live in a world where Grid Layout is in the CSS standard and widely accepted by browsers. I created a "stage" of 1600x1200 pixels wide, 2x the classic 800x600 recommended by webpages everywhere in a certain era and now just a bit smaller than what my screens deliver. This was a good fit, because it should extend over the page limits a little bit, and people can wonder what they are missing. Also users have control over zooming in or out of their browsers, for the super-curious seeking to know where the boundaries are.

I don't have much more to add about that, other than to repeat: Grid is a blessing. CSS is so good these days. 

## The actors (gifs)

For this project, I had to recruit a few hundred actors. This was easy thanks to [gifcities.org](http://gifcities.org), Internet Archive's gift to the world, a freetext search of gifs from the Geocities corpus. This has been fueling my presentation decorations for years! In terms of the collecting aspects to this, I just went with my gut -- I was there as a user, after all, so I feel like I have a good idea of gifs I'd encounter floating around different Geocities neighborhoods. I could probably write a long bit about this if I were in the process of getting an advanced humanities degree, but I am not.

I did learn a bit about gifs within the context of their emerging culture (lol what did I just say?), though, but I have more things to look at, maybe at the bit-level? Something I want to look into with this little series of gifs is how they load in low-bandwidth settings. Most people know that GIFs seem to loop forever, but maybe they loop for a finite amount of times. I think some GIFs have been optimized so that they load the first frame and then work on loading the rest of them, rather than popping into existence all at once. But maybe all GIFs load in this way. I saw a couple of GIFs, when I ran them through a hex reader, self-describe as being optimized for Netscape 2.0, like that was a flavor you could select in order to make GIFs especially for the web. I'd like to dig into all of that sometime in the future because it's super interesting!

## Some questions I asked

I don't necessarily have the answers. My assumptions overall ended up being true, but I haven't yet taken the time to deeply understand this (mostly of interest of what I worry about in the next section of this blog post).

* When network is throttled, how is image loading determined?
* Is it by what's on the top of the page?
* Is HTML or CSS considered first?
* Assuming size is the same, what is the order?
* How are things chosen for the browser cache (when it's not just everything)?

I feel like I have the simple answers but I am interested in the deeper answers.

## Future of the browser

All of these components come together with the assumption that browsers will continue to deliver it in this specific way. So while this is a piece about the past, it is also about the present and the near-future. It relies on the page staying up, me paying my domain name provider and my hosting server bills. It relies on browsers agreeing to interpret CSS rules in the same way they do right now. It requires browsers to load images in the order they appear as HTML -- this is the one that concerns me the most, I think, because everything about the performance depends on this. 

I definitely have more thoughts, but those are my notes!