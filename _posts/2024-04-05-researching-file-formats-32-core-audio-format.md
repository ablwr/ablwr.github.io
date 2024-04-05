---
layout: post
title: "Researching file formats 27: Core Audio Format"
date: 2024-04-05 08:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Core Audio Format (CAF) is a file format for storing and transporting digital audio data. It's published by Apple. [Fully disclosed](https://developer.apple.com/library/archive/documentation/MusicAudio/Reference/CAFSpec/CAF_intro/CAF_intro.html), thoroughly, with helpful contextual statements. It was introduced in 2005. I am a bit surprised, but relieved. Apple is not known for their openness when it comes to their formats, standards, operating systems, et al. I've just returned to using macOS after a very long time away, and I've been struggling with mixing a work Macbook's keyboard shortcuts with my personal computer's Linux shortcuts. I don'get too hung up on optimizing my machine, but even the basics cause me to struggle (like, the shortcut for copy/paste are different by default). Anyway, that was a digression, apologies! 

The other Apple formats I've been working with have not been well disclosed at all, and I went into this one assuming I'd have to do the same ambiguous work. Having something concrete and confident can really make this work so much easier than having to guess around different corners of the internet, working with sources that are of questionable/layered authenticity.

This is a container for other formats, but I think there's too many to list out -- because it can be any number of them, and the list would be fairly exhaustive. This also makes it easier to answer some of the preservation questions, because the answer is "it depends on the codec, ask the codec!" (Between writing this and submitting this format for feedback, I did end up writing a good bit out -- I will update when that FDD is live on the Library of Congress site!)

Anyway, happy Friday, I'll leave you with this. My favorite part of the spec was this: Magic Cookie Chunk

"The Magic Cookie chunk contains supplementary (“magic cookie”) data required by certain audio data formats, such as MPEG-4 AAC, for decoding of the audio data. If the audio data format contained in a CAF file requires magic cookie data, the file must have this chunk." ([source](https://developer.apple.com/library/archive/documentation/MusicAudio/Reference/CAFSpec/CAF_spec/CAF_spec.html#//apple_ref/doc/uid/TP40001862-CH210-SW1))

