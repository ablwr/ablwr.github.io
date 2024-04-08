---
layout: post
title: "Researching file formats 16: Transport Neutral Encapsulation Format"
date: 2023-12-14 07:00:00 -0500
tags: [file formats, fdds]
---
This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [Transport Neutral Encapsulation Format](https://www.loc.gov/preservation/digital/formats/fdd/fdd000485.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

Following up from [EMLX from a few weeks ago](https://bits.ashleyblewer.com/blog/2023/12/01/researching-file-formats-14-apple-emlx-format/), we have Microsoft's special way of handling emails: TNEF! TNEF: "Transport Neutral Encapsulation Format."

TNEF is responsible for the millions of people that have been annoyed at receiving an email with an attachment that doesn't mean anything to them: the winmail.dat attachment. Turns out, this just is Outlook talking to other Outlooks about whether Susan from Accounting is using Papyrus in her email signature, stuff like that.

Is TNEF responsible for "[the J](https://office-watch.com/2017/outlook-discovers-emoji-goodbye-j-hello-color-smiley/)"? Absolutely wild it took until 2017 to fix this. 

The answer to the question about the J was that it was Wingdings. So actually, well, maybe yes, because TNEF is responsible for sending richtext emails instead of plaintext, and it would have the intel to use Wingdings instead of a normal font, and a plaintext would just be the J. Hey! I had to talk that one out to myself but yeah, I guess TNEF is at play here!

It's just another one of those things that Microsoft does that makes official things feel like a spam or phishing attack. 

It also managed attachments, so it seems to have caused some trouble there, too. 

I'm feeling a little blessed because I looked in my email history and only saw five threads that included an attached winmail.dat.

Okay, I have story here that is a little related to TNEF. Probably ten years ago, I was working on a project and for some reason we were passing a file back and forth through email instead of using Git, and this file was a CSV file. Git was involved too, but for some reason we were temporarily not using it -- maybe because it was an open source project and we had to get the data in order before making it public, but the repo was already public? I honestly don't remember. But there was a problem with the file, it'd come back with some extra invisible newline characters. And the person sending me the file was like "hey, stop doing that!" and I was like "I'm not doing anything! You stop doing that!" We both were on macOS and we were also both using the same text editor with the same settings. So it turns out that it was the mail server that was intercepting our CSV, adding the extra linebreaks (which Microsoft will do), and sending it along, messing up the communication between an otherwise non-Microsoft connection. Annoying and invasive, right? I don't know that this was what I specifically ran into, but you can see a similar annoying problem in the [top answer to this stackoverflow question](https://stackoverflow.com/questions/10401863/how-to-send-a-csv-attachment-with-lines-longer-than-990-characters).


