---
layout: post
title: "Twitter Bots 5: Scheduling tweets with Cron"
date: 2014-06-29 21:24:56 -0400
comments: true
categories: [twitter bots, side projects]
---

Cron is a software utility that is used to schedule actions in time. It's great for handling reoccuring tasks. Twitter bots use a Cron statement to generate a tweet regularly. Cron tasks are super useful, but the syntax can be a little confusing and hard to remember.

The default bot tweets once a day, which is represented by ` 0 0 * * * `

I changed my bot to tweet once an hour, which is represented by ` 0 * * * * `

If I want my bot to tweet every hour from 9-5 on weekdays, it would look like ` 0 9-18 * * 1-5 `

Are you scratching your head? How can those numbers and letters mean anything?

In a row of five ( * * * * *), numbers break down like this: 

  1. Minutes 2. Hours 3. Day (of month) 4. Months 5. Day (of week)

That makes sense. Sort of. Except for having two different ways to represent time in a day, especially when they are not next to each other! Day of the month can be any number between 1-31 and is contingent on the month field. Day of the week is any number 0-6 and represents Sunday-Saturday.

The astericks means "every." If a field has an astericks, it will trigger the event at that time interval. 

Expressions aren't limited to asterisks and numbers. Other special characters include the slash (`/`), the comma (`,`), and the hyphen (`-`). The slash is used for increments of ranges. If I wanted to schedule an event to occur every five hours, I would use the string `0 */5 * * *`. Commas are used to separate items in a list. If I wanted an event to occur five minutes past the hour and five minutes before the hour, I could use the expression `5,55 * * * *`. Hyphens denote ranges. If I wanted to schedule an event to occur at the top of every hour during the Monday-Friday workweek, I would write `0 0 * * 1-5`.

If you don't want to figure out all of this syntax and just want to stay a die-hard Rubyist, you can also just install the gem "whenever" ([available here](https://github.com/javan/whenever)). Another way to integrate Cron syntax into Ruby apps is the gem [Rufus-scheduler](https://github.com/jmettraux/rufus-scheduler).

Important note: If you are updating your bot's Cron settings, you have to re-run the archive and modeling files to see reflected updates. 

---

More info:

[Cron on Wikipedia](http://en.wikipedia.org/wiki/Cron)
 
[RailsCasts #164 Cron in Ruby](http://railscasts.com/episodes/164-cron-in-ruby)

