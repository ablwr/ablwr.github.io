---
layout: post
title: "The bots are coming! Twitter bots!"
date: 2014-06-24 23:10:17 -0400
comments: true
categories: [twitter bots, side projects]
---

When I accepted a spot in the Flatiron School Ruby005 class, I knew my social life and, uh, casual internet-browsing life (?) would be cut dramatically down while I would be focusing all of my efforts on learning Ruby. I didn't want my friends to miss me too much (which is hard, since I also had to move from South Carolina to New York), so I decided to build a twitter bot that could tweet and talk to my friends.

Fortunately, there's already a Ruby gem that does all of the work for me. So I didn't really have to build a bot, I could just launch one! I used the gem found [here](https://github.com/mispy/twitter_ebooks) and pulled in the example bot's code. When I got stuck, I referenced [this bot tutorial](https://github.com/ScaryEnderman/Twitter-Bots-Tutorial). Setting up the bot and modifying the code was easy, but I hit a few snags trying to cooperate with the Twitter app API and OAuth.

Here's how the twitter_ebooks gem works.

1. The gem pulls in your twitter history in json format. 
2. Then, it parses through the json data and identifies words and phrases according to grammatical structure. 
3. It randomly generates sentences based on a user's tweet history. A cron job is set up to tweet randomly once a day, but I bumped that up to once an hour.
4. It knows how to respond to other users when they tweet at the bot.
5. It has a keyword list and will favorite or retweet tweets in its timeline that use those keywords.

Here are a few examples of what my bot has to say:

<blockquote class="twitter-tweet" lang="en"><p>CSS is in this instance, or is, at minimum, I&#39;ll take 6.</p>&mdash; ¡ɹǝʍǝlq ʎǝlɥs∀ (@ablwr_ebooks) <a href="https://twitter.com/ablwr_ebooks/statuses/481632877323354112">June 25, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet" lang="en"><p>...Damn it, iPhone, I hate it when you get a job at a grocery store.</p>&mdash; ¡ɹǝʍǝlq ʎǝlɥs∀ (@ablwr_ebooks) <a href="https://twitter.com/ablwr_ebooks/statuses/480258821844377600">June 21, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet" lang="en"><p>Tumblr adding fake film grain, tulips, u-matic tape players, cleaning my ears with a q-tip, maps...</p>&mdash; ¡ɹǝʍǝlq ʎǝlɥs∀ (@ablwr_ebooks) <a href="https://twitter.com/ablwr_ebooks/statuses/479307552946421762">June 18, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

But the best part of having a Twitter bot is that it can interact with other users! Classmate [Randall](http://randallreedjr.com/) asked her for some advice:
<blockquote class="twitter-tweet" lang="en"><p><a href="https://twitter.com/ablwr_ebooks">@ablwr_ebooks</a> What should I do this weekend?</p>&mdash; Randall Reed Jr. (@randallocalypse) <a href="https://twitter.com/randallocalypse/statuses/480034237391704064">June 20, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
<blockquote class="twitter-tweet" data-partner="tweetdeck"><p><a href="https://twitter.com/randallocalypse">@randallocalypse</a> I hope this suggests a return of the insane hotels.</p>&mdash; ¡ɹǝʍǝlq ʎǝlɥs∀ (@ablwr_ebooks) <a href="https://twitter.com/ablwr_ebooks/statuses/480034319030026240">June 20, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>


That's my bot! Have your bot add my bot at [@ablwr_ebooks](http://www.twitter.com/ablwr_ebooks). Stay tuned for some more technical blog posts about working through the Twitter authentication steps, understanding CRON, modifying a bot, deploying to heroku, and ~mad science experiments~.



 