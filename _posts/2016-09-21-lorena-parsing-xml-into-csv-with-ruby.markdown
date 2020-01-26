---
layout: post
title: "Parsing XML into a CSV with Ruby"
date: 2016-09-21 15:16:37 -0400
tags: [teaching, programming]
---

So a short while ago, my friend Lorena posed this question...

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Question: can I grab a XML &amp; convert that to a .csv? or better yet can I grab certain parts of the XML and redirect to a .csv? <a href="https://twitter.com/hashtag/howto?src=hash">#howto</a> <a href="https://twitter.com/hashtag/help?src=hash">#help</a></p>&mdash; Lorena Ramírez-López (@DaleLore) <a href="https://twitter.com/DaleLore/status/773625570374590464">September 7, 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

And thought "ya, I know how to do that and I also have a secret agenda to get all archivists to learn Ruby." I sent her some pseudo-code but it's better to follow up in a blog post that actually explains how things work (also, that pseudo-code would *not* have run).

If you want to play along at home, here is the small ruby script: [https://gist.github.com/ablwr/aad01782214cec1632b65bc42559d4ca](https://gist.github.com/ablwr/aad01782214cec1632b65bc42559d4ca)

And here is the sample xml: [https://gist.github.com/ablwr/850638dc5c6a62aef6e1c9bb140bf107](https://gist.github.com/ablwr/850638dc5c6a62aef6e1c9bb140bf107)

I'll walk through the lines and explain them accordingly.

First we have to set some things up.

```
require 'csv'
require 'nokogiri'
```

Ruby has extra libraries and we will need two of them. One is the CSV library, which comes with Ruby. The other is the Nokogiri library, which can be hard to install but it lets you manipulate XML easily (including HTML). This is telling the script to grab things we need so we can do it the easy way.

A lot of computers already have Ruby installed. Nokogiri takes extra steps (and sometimes will blow up in your face). So this script won't work until you [install Nokogiri](http://www.nokogiri.org/tutorials/installing_nokogiri.html). This might be a total nightmare but it also might be totally fine. If you send me error messages, I can send you my secret girlscout techniques to fix it.

To run a Ruby script, you can type `ruby /path/to/script.rb` in your command line interface of choice.

Next, we need to get our XML and get it in shape.

```
xml = File.read('hello.xml')
doc = Nokogiri::XML(xml)
```

I am running this script in my root directory (`cd ~` gets you there on a Mac) and the XML file is also saved there. If I downloaded this .rb file and hello.xml and they saved to my Downloads directory, I could still run this script from my root directory, but run it by changing the File.read to File.read('Downloads/hello.xml').

So we read the document but then we have to turn it into a special Nokogiri document so we can easily grab what we need. That's what the second line is doing, and later we can work on grabbing info out of the variable we just named "doc".

```
all_the_things = []
```

Scoping is important in programming languages, including Ruby. This makes a variable in advance, and the brackets mean it is an empty array. When we fill up this `all_the_things` later, it will be ready to go.

```
doc.xpath('//file').each do |file|
  title          = file.xpath("./title").first.text
  filename       = file.xpath("./name").first.text
  identifier     = file.xpath("./identifier/*[contains(text(), 'My display ID')]").text
  secret         = file.xpath("./identifier/secret").attr('secret').text
  all_the_things << [title, filename, identifier, secret]
end
```

This chunky bit of code is where we go through our first loop using the Nokogiri library...

We have our `doc` and we know that it is a `<document>` full of many `<file>`s, so this first part -- `doc.xpath('//file').each do |file|` is where we start off our loop and grab (using xpath) every XML node that is a `<file>`. Then we start grabbing the things that we need. We can grab a bunch of stuff, like the title, the file name, and some identifiers. Nokogiri builds on Xpath statements which are good for all archivists to know, since archivists are obsessed with XML. These are saying "give me the first `<title>`", "give me the first `<name>`", "give me the identifiers that has the phrase My display ID in it" (this is an example of having to grab data out of poorly-formed XML -- who would do this?!), and "give me the secret attribute within the secret identifier". You can see how this is all arranged in the [sample XML](https://gist.github.com/ablwr/850638dc5c6a62aef6e1c9bb140bf107).

```
CSV.open('new_file.csv', 'wb' ) do |row|
  row << ['title', 'filename', 'identifier', 'secret']
  all_the_things.each do |data|
    row << data
  end
end
```

This will save *in the directory you ran the script in*. Which, like I mentioned earlier, will only work if you are in the same directory as the hello.xml, unless you change the above file path.

The `'wb'` flag is added to let Ruby know that we are going to be **w**riting to the file, not just opening it, and that we want to make sure it opens in **b**inary mode (although running it without the `b` flag is probably fine).

So this is our second loop and it has another loop inside of it. It's OK to feel dizzy. When you open a CSV, it's ready to work row by row until you've had enough and tell it to stop. First I ask it to make a row with column titles, which is what `row << ['title', 'filename', 'identifier', 'secret']` is all about. The `<<` is "shoveling" these strings of text into the first row. I kinda think of it as having a Mary Poppins bag that looks like this `[]` and then you can just `<<` to add things in there but it pretty much stays the same size because it's whatever you named it. Ours is named `all_the_things`.

So I take our `all_the_things` and I know all of our XML data has been living there for a minute, floating around in magical Mary Poppins Computer Bagspace, so I tell it to take every array inside the array and make one row for every array. Sorry -- Nested arrays are confusing so that might need to sink in for a minute. The array looks like this: `[["The first file", "one.mkv", "My display ID: 1", "sesame"], ["The second file", "two.mkv", "My display ID: 3", "benne"], ["The third file", "three.mkv", "My display ID: 3", "goma"]]`. Everything is lined up perfectly and ready to become CSV rows.

Anyway, we close up our two loops and that's...

The end! That is it! Assuming you didn't give up while your computer objected to installing the Nokogiri gem, you should have a beautiful little CSV (if CSVs can ever be considered beautiful -- archivists are out of control).

BYE

Here are some bonus resources!

* [Ruby CSV library documentation](http://ruby-doc.org/stdlib-1.9.3/libdoc/csv/rdoc/CSV.html)
* [Nokogiri documentation](http://www.rubydoc.info/github/sparklemotion/nokogiri)
* [Nokogiri/Xpath cheatsheet](https://github.com/sparklemotion/nokogiri/wiki/Cheat-sheet)
* [Ruby file-opening modes](http://ruby-doc.org/core-2.3.1/IO.html#method-c-new)