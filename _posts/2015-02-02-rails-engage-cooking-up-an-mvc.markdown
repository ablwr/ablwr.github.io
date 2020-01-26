---
layout: post
title: "Rails Engage: Cooking up an MVC"
date: 2015-02-02 21:14:34 -0500
tags: [rails engage]
---

![](http://i183.photobucket.com/albums/x54/TrueX-Ray/TNG%20Caption%20This/TNGCaption158e.jpg)

Okay! Last time we talked about the magic of `rails generate` and the structure that gets created when you make a new Rails project. I gave you a soft warning to pay close attention to the app/ folder with the foreboding "Just remember the MVC"... Now let's talk about the MVC.

I'm not the only person to use this analogy, but here it goes and I know you'll be able to relate to it. The best way I've found to understand MVC is to treat the framework like a restaurant.

The restaurant is broken up into three parts: Chefs working behind the scenes to make a great meal, servers that deliver the meal to the customers so they can eat it, and plates/tables/utensils so the meal can be enjoyed. Your app is THE MEAL!

**Models** -- **Chefs**

Models hold the code. They hold the logic. They are the brains of the operation. A master chef has to take all of the individual pieces of something and put them together just right to make something delicious.

**Controllers** -- **Servers**

The chef is too busy making a masterpiece to give her customers the meal herself! She's got work to do! The controllers help keep all the beautiful, well-crafted meals going out to the right customers. Being a server (the restaurant kind) is hard work, keeping track of what everyone ordered and where they are seated. The controller takes data from the model and delivers it to the plate.

**Views** -- **Plates**

Yum yum, time to eat these snacks up, right? The view is where all the front-end work comes into play. It's a very important component because just because you have a delicious meal, no one is gonna come to your restaurant if its lookin' like the Wing Basket. Or maybe they will and it'll be the best kept secret in town. Anyway, the view is dedicated to make all your hard work and code look great so people will actually want to consume it.

MVC is a good framework to know, but what's the point? The point is to keep your code clean. Coding means juggling a lot of different things at once, so this framework helps you figure out where you need to go to find your problem and fix it. Is your math not working? Check your models. Is the math being delivered to the wrong page? Check your controllers. Is the math problem just super ugly? Take a look at your views. 

There a lot of nuances here, but this is a good overview to have in the back of your mind as you write code. And remember, the first goal is to get things working so if you accidentally put some logic in your view, don't sweat it.