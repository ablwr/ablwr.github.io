---
layout: post
title: "Considering Rust ...for Video"
date: 2018-04-10
tags: [recurse center, rust, video]
---

This is a follow up on my [last post](http://bits.ashleyblewer.com/blog/2018/04/09/considering-rust/). After playing with Rust for the first time last Saturday (thanks Casey), I did a whole bundle of reading about it the next day, Sunday. I also got some tips from [Kieran O'Leary](https://twitter.com/kieranjol) on some work that had been done in the open source media space with Rust and that sent me into a spiral and flooded my [RC syllabus](https://github.com/ablwr/my-recurse-center-syllabus) with links.

I had originally intended to see this project through in C because FFmpeg is written in C, and [MediaConch](https://mediaarea.net/MediaConch) and [QCTools](http://github.com/bavc/qctools) are both written in C++/Qt and I've dug around in those codebases before and worked alongside them pretty extensively. So I went in with the mindset that C is the best choice.

But the point of me taking what is essentially a sabbatical to build a video codec is primarily for educational purposes, so really I can do whatever I want. INCLUDING ABJECT FAILURE!

And what do I want? I'm [switching to Rust](https://www.rust-lang.org/en-US/), and here's why!

- I don't know either, so the default learning curve is extremely steep no matter which one I go with.
- I don't know shit about memory allocation (although it does sound fun! but also, life is short?)
- Debugging tools: Explored this in C last week and felt grumpy and confused at what was causing the problem with even running the debugging tools: Me? macOS? Homebrew? gcc? gdb? Wrong version of C? Wrong parameters? The code itself? Explored this in Rust this week and still felt grumpy at myself, but the compiler is extremely good at giving me error messages and telling me what's wrong and precisely where I am wrong (and oh boy, it has a lot to say). 
- Rust even has a "clippy" feature that will give you "helpful hints" about your code. THE COMPILER CAN ALSO BE A LINTER!
- Community matters! And I've been really impressed by the efforts made by the Rust core team and sponsoring organization Mozilla to create good community and great documentation alongside code stability and cleverness.
- [https://crates.io/](https://crates.io/)
- Firefox and VLC both have Rust underneath now!
- Can always dip down into C

And finally, the contestable one, is that it is totally possible to write optimal, production-ready, multimedia-quality code in Rust. Am I going to be writing that kind of code? No, definitely not. I can barely write a function and don't even understand the basics of reading math equations that require Pandoc to be rendered to the screen. I hope to be able to correct a little bit of that in the next 11 weeks, but I am also realistic.

I'm looking forward to digging into [Rust-AV](https://github.com/rust-av/rust-av), a "Pure-rust implementation of multimedia primitives and eventually demuxer, muxers and codecs" by [Luca Barbato](https://blogs.gentoo.org/lu_zero/2018/02/14/rust-av-rust-and-multimedia/) and Kostya's work on [NihAV](https://codecs.multimedia.cx/2017/06/nihav-concept-and-principles/), another personal-project multimedia framework in Rust. I'm glad people who are legit-experts on these subjects are giving this a try too and blogging about it.

Okay, time to start writing words and back to writing code (which actually means frowning and squinting at my computer reading error messages).

Advice is welcome!