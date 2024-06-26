---
layout: post
title: "Rails Engage: Setting up your environment"
date: 2015-01-11 09:11:48 -0500
tags: [rails engage]
---

![Data using a computer](http://38.media.tumblr.com/f360873af12a76bc4b00a549c799a2d1/tumblr_mtayo9M8JJ1rik14zo1_400.gif)

![Data using a computer fast](http://38.media.tumblr.com/bb28f80f960d040e9d2842fed6d20ab9/tumblr_mtayo9M8JJ1rik14zo3_400.gif)

 Disclaimer: I love this part. I love setting up environments, I love debugging problems on the command line\*, and I love working on server-side problems. Ever since I was a kid. Weird, right? Most people don’t feel that way (or lacked the opportunity). And it’s hella intimidating to start your coding journey by having to stare at a huge black screen\* that you don’t understand. I also used DOS when I started using computers, so it was comforting to me, a familiar screen, and even working in the terminal\* now gives me this strong sense of nostalgia for childhood. SO NERDY. Most people have only used graphical user interfaces to interact with their computer, so typing things into the shell\* is definitely weird.

Weird and scary. Because you're looking at an empty black box, typing into the darkness, it can be intimidating because of a slight fear that you'll do something wrong and ruin your entire computer. This is highly, highly, highly unlikely. Everyone starting out gets the disclaimer of being wary of commands that start with `rm` (remove), and you could end up in black holes that takes a few hours to get out of because of debugging, but be brave and go forth! Environment problems don't take a long time because you are stupid. They take a long time because the computer is stupid and needs explicit instructions.

It seems like programming is a lot like the opening gif, up above. You don't have to be Commander Data to use the command line, though. And a lot of environment setup involves pressing a button and waiting a while. We're gonna have you up and running like this... in theory.

![Data pressing a button](http://38.media.tumblr.com/ed6df7c82c24e812dfe3c5892a65bcb8/tumblr_mohoyw4X0l1s67vyfo4_250.gif)

The final and most difficult part about setup is that in theory it’s easy. In theory, you just run a few lines and everything is totally fine and your computer is like :) complete! :) installed! :) good! :). But most of the time, you get some crazy  jargon.

First rule: Read what the computer gives back to you! This is the best thing you can learn from setting up your environment (assuming you run into problems). Your computer will tell you what’s wrong. Sometimes it’s good at articulating its feelings. Sometimes its not so good. It just a computer, after all. It doesn’t really have feelings. But when you get an error message, don’t panic!

Second step: If you have no idea what the computer is trying to tell you, google it. Google the shit out of it. Copy-paste that shit right into google and you’re most likely to get a link to StackOverflow with someone else that had your same problem. Especially when you’re learning early on — at least one person, usually many people, have had the same problems you are having right now. And some kind person out there, again usually on StackOverflow, has already gently explained the right thing to do in order to fix it. If you don’t understand what they are saying, keep scrolling or start googling what they are saying. Just google forever. Or use your preferred search engine.

Enough of these steps, let's get practical. Pop open that terminal open! (Use Spotlight to search for Terminal, or you can find Terminal.app in your applications folder **in the Utilities folder**). Windows users, sorry I am leaving you in the dust here.

First, let's install [Homebrew](http://brew.sh/). Follow the commands on the page and listen to anything the command line gives back to you. Homebrew is great. It's a package manager. What does that mean? It means you can add things to your computer that you need without having to do all the work yourself, or running into problems. So when you want to install a new programming lanuage or component, you can do it with one line. Overall, from a new-user perspective, it helps protect your machine from you. It makes command-lining like a wild beast (as a new user) much safer.

![beer](http://emojipedia.org/wp-content/uploads/2013/07/160x160xbeer-mug.png.pagespeed.ic.kOjM-Un-7l.jpg)

I think you might need to install X-Code. This will vary based on your operating system. See the resources below if you have trouble doing this. 

When Homebrew is up and running, you can use it to install Ruby, RVM (this manages), and Rails by running `brew install` and the thing you want to install. Rather than repeating how to do this from memory, I recommend following the guides I link to at the bottom of this post. 

\* I realize that people commonly use several words to refer to the same thing: that black (by default) screen you use to manipulate your computer, with only text on it. On OS X (Mac) operating systems, the application is called **Terminal**. Inside, it uses the **shell** (Unix term for a user interface for accessing your computer). There are a few language structures used in shell, but the most common (and default) is called **bash** (which is a free, open-source alternative of the Bourne shell, which is why bash stands for Bourne-again-shell). All of this brings together the ability to manipulate your computer via the **command-line** (as opposed to using your mouse to click where you want to go — that uses the graphical user interface). 

Windows is a different beast, of course, but it might be the beast you are stuck with. On Windows, you are looking for the Command Prompt (found via this path: Start > All Programs > Accessories > Command Prompt, if I recall correctly).

![clinking beer](http://emojipedia.org/wp-content/uploads/2013/07/160x160xclinking-beer-mugs.png.pagespeed.ic.Gv-8d6e0qe.jpg)

Although most learning can be done alone, it's a bit of a bummer that setting up the environment is like being forced to dive head-first into the deep end without even ever having been in the water before, much less know how to swim. If you are a non-Marleigh following along with these posts, it's best to try to find a friend or resource that can sit next to you and explain things. If you have no friends (that know about this stuff), you can ask me! But remember firstly that search engines are also your friend.

### Resources:

[How to Install Xcode, Homebrew, Git, RVM, Ruby & Rails](http://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/) 
 
[Braumeister -- list of different brew packages](http://braumeister.org/) 
 
[X-Code](https://developer.apple.com/xcode/) 
 
[Rails Guide: Getting Started with Rails](http://guides.rubyonrails.org/getting_started.html) 