---
layout: post
title: "Making a Matroska Magic Hat"
date: 2018-04-02
---

Hello! This blog post is going to scratch an itch I've had for a long time and really don't know what prevented me from doing this when it first occurred to me years ago because it's very simple. The itch is storing a Matroska file inside a Matroska file. This will go into the steps I took to make the file and what you might be able to do with it later.

You will need [FFmpeg](http://ffmpeg.org/) and [MKVToolnix](https://mkvtoolnix.download/) to create the files, add attachments, and investigate the files. I also use [MediaInfo](https://mediaarea.net/en/MediaInfo).

First, find a picture of a cute rabbit on the web and save it to your working directory as rabbit.jpg. Then, turn that rabbit into a video -- magically -- using FFmpeg! 

`ffmpeg -r 1 -loop 1 -i rabbit.jpg -t 10 rabbit.mkv`

Then do the same with a magic hat!

`ffmpeg -r 1 -loop 1 -i magic-hat.jpg -t 10 magic-hat.mkv`

Then, to get your rabbit into the hat, it's as easy as...

`mkvpropedit magic-hat.mkv --add-attachment rabbit.mkv`

Is it there? Let's take a (verbose) look: 

`mkvinfo -v magic-hat.mkv`

![magic hat](/images/magic-hat.jpg) 

Yup! Don't trust mkvinfo? Try mediainfo:

`mediainfo magic-hat.mkv` 

![magic hat](/images/magic-hat2.jpg) 

It's also available in a hex editor. This is the second Matroska file's magic numbers, which are `6D 61 74 72 6F 73 6B 61`.

![magic hat](/images/magic-hat3.jpg) 

And now you have a rabbit in a hat, a Matroska file inside of a Matroska file! It's pretty hidden -- only one line in MediaInfo and doesn't appear in the default settings for MKVInfo. Running `file` on the file is only going to tell you: `magic-hat.mkv: Matroska data`. 

But this rabbit is still hidden inside the hat -- what if you want to really make some magic? How do you get the rabbit out of the hat?

`mkvextract magic-hat.mkv attachments 1` 

This will get the rabbit back out of the hat. But it doesn't just get the rabbit out of the hat, it creates a copy of the rabbit that lives inside of the hat.

In one not-so-clever line, pull the rabbit out of the hat and play it for two seconds before hiding the rabbit again (aka deleting it):

`mkvextract magic-hat.mkv attachments 1; ffplay -t 2 -autoexit rabbit.mkv; rm rabbit.mkv`

But is there a better way to pull the rabbit out of the hat? 

The Matroska specification says:
`Matroska Readers MUST NOT execute files stored as Attachment Elements.` 

Sooo... maybe we'll have to get creative when really pulling the rabbit out of the hat, which I'll save for another day.

To wrap up, what are the implications of this? What are the ramifications of this? Does this have any practical purposes whatsoever? I don't know, but I am happy to easily hide files inside of files.

Resources:
- [Library of Congress Formats: Matroska Multimedia Container](https://www.loc.gov/preservation/digital/formats/fdd/fdd000342.shtml?loclr=blogsig)
- [Matroska Specification](https://github.com/Matroska-Org/matroska-specification/blob/master/attachments.md)
- [mkvtoolnix documentation](https://mkvtoolnix.download/docs.html)
- [ffplay documentation](https://ffmpeg.org/ffplay.html)

