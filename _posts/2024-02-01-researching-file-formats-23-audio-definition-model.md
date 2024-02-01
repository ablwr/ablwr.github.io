---
layout: post
title: "Researching file formats 23: Audio Definition Model"
date: 2024-02-01 07:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

This format is about audio, but it's a text-based document that describes audio. You can say it _defines_ an _audio model_. It is typically stored as XML, but JSON is a valid option, too. While the rest of the software engineering field goes "ick" when it hears about XML, both the cultural heritage sector and audio/video media engineering sector still use it heavily.

ADM is coming out of research from the [European Broadcasting Union](https://adm.ebu.io/), which have other hits like [EBUCore](https://tech.ebu.ch/metadata/ebucore) for describing media elements. The idea behind ADM is to standardize how audio is stored, inspired by the rise of extra high-def sounds (like, going beyond Dolby 5.1). Where does it go, physically? Or are there different language tracks? If so, what are the order? Stereo and/or mono, or something else? 

Formally, "Audio for broadcasting and cinema is evolving towards an immersive and interactive experience, which requires the use of more flexible audio formats. A fixed channel-based approach is not sufficient to encompass these developments and so combinations of channel, object and scene-based formats are being developed" ([source](https://www.itu.int/dms_pubrec/itu-r/rec/bs/R-REC-BS.2076-2-201910-I!!PDF-E.pdf))

BBC R&D seems like they are quite invested in this format, making a [toolkit for ADM usage](https://www.bbc.co.uk/rd/publications/audio-definition-model-software).

If interested in more, here are some of the resources to check out:
- International Telecommunication Union. "[BS.2076 : Audio Definition Model](https://www.itu.int/rec/R-REC-BS.2076/)"
- BS.2076 : Audio Definition Model": Recommendation BS.2076-2 (10/2019). This is a direct link to the English PDF of the [latest standard](https://www.itu.int/dms_pubrec/itu-r/rec/bs/R-REC-BS.2076-2-201910-I!!PDF-E.pdf).
- European Broadcasting Union (EBU) [ADM elements reference](https://adm.ebu.io/reference/elements_intro.html)
