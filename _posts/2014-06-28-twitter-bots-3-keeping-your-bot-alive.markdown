---
layout: post
title: "Twitter Bots 3: Keeping your bot alive"
date: 2014-06-28 20:31:52 -0400
comments: true
categories: [twitter bots, side projects]
---

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p><a href="https://twitter.com/wetted_ashes">@wetted_ashes</a> <a href="https://twitter.com/ablwr">@ablwr</a> Just spent too much time coding and having so many excellent things to read thanks to <a href="https://twitter.com/hashtag/timezones?src=hash">#timezones</a></p>&mdash; ¡ɹǝʍǝlq ʎǝlɥs∀ (@ablwr_ebooks) <a href="https://twitter.com/ablwr_ebooks/statuses/478713633023602688">June 17, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>


Once a Twitter bot has been configured, it has to stay running in order to stay alive. And for that, it needs a server. When I was debugging my bot, I was running it off of my computer and got notifications of activity in my terminal. This works if I want my bot to only be active when I am active, but I want my bot to be available all day and night! 

The most logical way to do that would be to deploy my bot's code to a Heroku instance. It's free and super easy, especially if you already have a good grasp on git workflows. Basically you just have to...

```
git init
git add .
git commit -m "BOTS"
```
then,
```
heroku create
git push heroku master
```

That's it! That is it. Actually, that is not it, because I had to log onto the heroku web interface and adjust the Dynos worker to 1 instead of 0.


['heroku page'](/images/herokurunner.png)


 But after that, my bot was again operational and back to her normal (myself)
self.

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p><a href="https://twitter.com/ablwr">@ablwr</a> <a href="https://twitter.com/trlwagner">@trlwagner</a> The pass is lurking in the reboot, everyone get renewed at 21, and I do not like that.</p>&mdash; ¡ɹǝʍǝlq ʎǝlɥs∀ (@ablwr_ebooks) <a href="https://twitter.com/ablwr_ebooks/statuses/478715343737602049">June 17, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
