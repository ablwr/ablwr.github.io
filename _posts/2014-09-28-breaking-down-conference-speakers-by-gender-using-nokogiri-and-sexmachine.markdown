---
layout: post
title: "Breaking down conference speakers by gender using Nokogiri and SexMachine"
date: 2014-09-28 14:32:49 -0400
comments: true
categories: [weekend projects, Ruby, Nokogiri, Sex Machine, data]
---

Last week, I was in converesation with some peers in the moving image archiving, preservation, conservation, (et al...) field and we were discussing ways to improve and empower the roles that women in the field have. One of the things that came up was it'd be interesting to see the breakdown over time of the people presenting at the annual [Association of Moving Image Archivists](http://amianet.org) [conference](http://www.amiaconference.com) and whether it was appropriately stacked in terms of gender.

With around 200 speakers, it would be great if I could just grab this data algorithmically and not have to parse it piece-by-piece using my slow human brain! Over the weekend, I went to work combining Ruby web scraping tool, [Nokogiri](http://nokogiri.org/), with a library that does a pretty good job at determining probable gender based on first name ([SexMachine](https://github.com/bmuller/sexmachine)). It was fun to wrangle data around, but not without conflicts.

Some problems:

1. I wrote a parser for the most recent conference’s webpage, but that parser can’t be used for previous conferences. The layout for the previous year is different from the current layout, and the year before that is available only as a .pdf. The years prior to that aren’t (immediately and openly) available at all!

2. The website was not marked up in a way that made it easy to pull in only the speaker names. I had to throw in a lot of remove-if exceptions because I was basically having to pull in anything that was in a p tag and removing very long strings and very short strings (and a few other things).

3. Obviously gender is a larger spectrum than the binary male-female and assessment via name is not an ideal method, but I'm just playin' with data here! I think the results will still hold value, but I always feel a little bit icky when I also have to push things into a gender binary.

I can now take the rough breakdown of the data and just modify as needed. To do more complex problems, though, will involve more than just the parsed names in arrays separated by arrays (see below).

I’m not going to be able to pull out the precise data I want, but it was fun project and I was excited to spend a few hours writing (and thinking) in Ruby again, which I hadn’t really had the opportunity to do in the past month or so (it’s been all Javascript and front-end work around these parts). 

Side note: Didn’t someone recently run a quick check on the gender breakdown of published authors in The Moving Image? That data is easier to grab because there’s less of it.

Plans going forward:

1. Run quick analysis on the organization’s membership directory to get a rough idea of the overall distribution of the field.

2. Break data down with and without consideration to one person speaking multiple times. (Which is better to consider?)

3. Break data down with consideration to time chunks and weighing one person speaking for a full block of time differently than seven people speaking in the same block of time. (Side-consideration to assess the value of poster presentation time). This involves getting down with statistics and math.

4. VISUALIZATIONS.