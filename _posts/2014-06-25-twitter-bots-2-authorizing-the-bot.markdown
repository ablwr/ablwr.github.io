---
layout: post
title: "Twitter Bots 2: Authorizing the Bot"
date: 2014-06-25 12:54:34 -0400
tags: [twitterbots, flatiron]
---

For me, the hardest part of getting a Twitter bot up and running was negotiating with Twitter's API keys and application settings. The primary reason for this was probably that I kept getting overly excited and jumping ahead, trying to finish the project too soon. I first set up an app by registering my primary twitter account. Turns out that wasn't necessary at all, and I could access and download my tweets just by using [twurl](https://github.com/marcel/twurl) to collect authenticate and grab my main account's twitter archive. I THINK. Those authentication details went into a hidden file, .ebooksrc, in my computer's main user directory. I know because I had to break into it several times and switch out the keys in order to get it to work, but most users shouldn't need to open it again, once it's in there.

To get the bot operational, I had to create an dev account and app using my bot's twitter account (oh yeah, I also had to register a new twitter account -- but that's obvious, right? I'm not talking to a bot, I'm talking to a human... right?)

Under My Applications (next to my user profile), I created a new app. Under the API Keys tab, I generated some access tokens. The consumer and OAuth details can then be added to the bot's bots.rb file, along with the bot's username and the bot model (in my case, my main twitter account).

```
CONSUMER_KEY = ""
CONSUMER_SECRET = ""
```

```
  Ebooks::Bot.new("") do |bot| # Ebooks account username
  bot.oauth_token = "" # oauth token for ebooks account
  bot.oauth_token_secret = "" # oauth secret for ebooks account

  make_bot(bot, "") # This should be the name of the text model generated from the base twitter account

```

Sounds easy, but I had such a hard time! Writing it all up, I am embarassed that it took me so many tries to get it right. My problem was that I first thought that the CONSUMER_KEY fields needed to come from my main twitter account instead of from the bot's account. Then, I changed the CONSUMER_KEY details but also changed the info in the .ebooksrc file. Then, I changed them both around again but didn't refresh my OAuth token.

The final step was that my bot was running but unable to do anything because the API Keys permission access level was set to read-only. It is not super-clear in the documentation, but the account generating the access token has to have a valid phone number associated with it in order to get granted permission for read/write/execute status. After confirming with a phone number, my bot was able to talk to people and generate its own tweets based on my model.

A final important debugging note: After changing the permission access level from read-only to read/write, you will probably have to regenerate the API keys and add the new codes to the app.

