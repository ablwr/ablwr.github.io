---
layout: post
title: "Do you like Blacklight but hate MARC? Roll your own instead!: Indexing your non-MARC data into SOLR!"
date: 2016-01-25 21:41:48 -0500
tags: [webdev]
---

[Blacklight](http://projectblacklight.org/) is a discovery layer intended for library catalog records, which is great. Hydra also uses Blacklight as its discovery layer. The foundation of Blacklight is built upon Rails and SOLR. Plus Bootstrap for style and Devise for user authentication. And the big bonus on top is easy MARC ingest to suit librarians. But what if you don’t have MARC records? After fussing around with getting SOLR to appreciate my beautiful, custom non-MARC data, I decided to just give up and do it myself. 

Usually that sounds like something that would end in a complete disaster, but I found that it was a lot easier to “roll my own” Blacklight using Rails, SOLR, and the gem `sunspot`, since I was using the tools I was already familiar with. I also didn’t need to set up Devise since user authentication wouldn’t be necessary for my purposes. Having worked with Devise before, I know it can get in the way (especially in the routes).

Because I was working with custom data, it was easy to import a CSV of that data right into a Rails model instantiated with all of the necessary fields.

After that, sunspot to the rescue! [Sunspot](https://github.com/sunspot/sunspot) makes indexing data into SOLR incredibly easy. It comes with built-in rake tasks that help take care of starting and stopping of the SOLR engine, which runs quietly in the background as you work and debug. It also comes with a rake task that can be used to reindex, also good while developing and figuring out what needs to go where.

For help with understanding sunspot, you could read the docs but I think you’ll have better luck, as I did, with [Ryan Bates’s RailsCast](http://railscasts.com/) episode on it. Seriously RailsCast has saved my ass so many times in making me actually understand how different code bases work.

Episode here: [http://railscasts.com/episodes/278-search-with-sunspot?autoplay=true](http://railscasts.com/episodes/278-search-with-sunspot?autoplay=true)

If the supplemental code at the bottom isn’t enough, more code is here: [https://github.com/railscasts/278-search-with-sunspot/tree/master/blog-after](https://github.com/railscasts/278-search-with-sunspot/tree/master/blog-after)

The docs are pretty good but I found that there were a lot of syntax idiosyncrasies that weren’t fully explained that had me adjusting my `searchable do` block over and over again. Aspects like `limit -1` are in the examples to show all facets, but doesn’t always work. These kinds of things had to be solved through trial and error. As a result of this, the code is also not very “DRY.” Which is okay with me because I’d rather have things that work and can be customized easily during the design stage over trying to be super-clever early on.

The difference between string and text also was not super clear to me, which might have been my own skimming fault. Tip: You can apply facets to strings. You can perform freetext search on text. I wanted both, so I had to index every column (oh yeah, I also wanted to index everything), I have to apply text and strings to every column.

After that setup is done, you can move into the controller.

First, set up facets!

```
facet :DocType
with(:DocType, params[:DocType]) if params[:DocType].present?
```

Then, set up search in a similar way:
```
fulltext params[:search]
 with( params[:category] ).equal_to( params[:search] ) if params[:category].present?
```

In the controller, setting `@videos = @search.results` will make it easy when moving to the next step, into the view.

For the view, fortunately I was just able to loop through all of the potential facets set in an array and build the facet column. Only a little bit of code is needed to display the search results: just loop through the results (`for row in @videos`) and (`style it up however`) and everything is set.

Here’s a couple of gifs demonstrating the final product, which is a database of testable Matroska videos for use with the [MediaConch project](https://mediaarea.net/MediaConch/), culled from ‘interesting’ Matroska videos uploaded to the [Internet Archive](https://archive.org/).

![](/images/mediaconch_repo1.gif)

![](/images/mediaconch_repo2.gif)

So, moral of the story: If you are thinking about using Blacklight but don't have MARC records, it might be easier to use `sunspot` and skip the cruft.