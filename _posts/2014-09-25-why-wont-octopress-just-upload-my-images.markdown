---
layout: post
title: "Why wont Octopress just upload my images"
date: 2014-09-25 13:04:20 -0400
tags: [programming]
---

*Why won’t Octopress just upload my images?!?!?!?!?!?!, or how I learned to stop worrying and love the source.*

![](/images/glitch1.png)

I’ve been using Git for a while and I feel like I have a good grasp on it. I’ve also been using Octopress for a while, integrated into Github pages, and I feel like I have a good grasp on it, too. Rake tasks, right? I’ve WRITTEN rake tasks before! I got this! But for some reason, uploading images for me always seemed like it was a miracle that would work sometimes and not work at other times. Y’know… computer magic.

![](/images/glitch2.png)

Sometimes it would just straight up EAT my images and I’d have to remake a screen cap and get angry and keep pounding my head against the code-wall. That’s dumb, though. That’s no way to solve a problem, especially when dealing with logical beasts that perform as instructed. But I wasn’t sure what I was doing wrong. I would just keep moving things around and committing until it seemed to give up and take my images.

![](/images/glitch3.png)

It’s just not a good way to live.

![](/images/glitch4.png)

Are you having this problem, too? I decided to figure it out.

![](/images/glitch5.png)

I was dropping my images in the wrong file! With Octopress, there are a lot of potential places to put images. It’s tempting to put it in public/images folder. It’s also tempting to put it in the _deploy/images folder. Those are bad, though. Those are bad. You want to put it in the SOURCE folder. If you stick images in source/images, they will get picked up when running rake generate / rake deploy. If they go anywhere else, the rake task doesn’t know what to do so it just overwrites them and your images will just disappear.

![](/images/glitch6.png)

Maybe this is a no-brainer, but sometimes I feel like a no-brainer, myself.

# P.S.

Another note! It's important to use the right syntax when adding images. One method in Markdown is to use this syntax:

 `![netflixforbooks](images/markdown.png)`

But for Octopress, you want to use this:

 ![](/images/markdown.png)

 
Otherwise, images will work on the front page of your blog but they won't work when you visit the individual pages. The more you know...!


