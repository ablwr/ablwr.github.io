---
layout: post
title: "Stealing snax using semicolons in Rust"
date: 2018-04-13
tags: [recurse center, rust]
---


Friends, colleagues, and enemies all know this about me: *I love stealing snax*. Stealing food from other people brings me such a true joy, which is also why if I were a Pokemon I would definitely be [Munchlax](https://bulbapedia.bulbagarden.net/wiki/Munchlax_(Pok%C3%A9mon)), the high-energy garbage-living pre-evolved form of Snorlax and also classified as a "Big Eater" pokemon. I am pretty sure the reason why my body can't digest gluten anymore is because a curse was put on me in my early 20s due to my love of snack-stealing, and now I can't steal snax as much as I used to. But the desire is still there!

Anyway, I was pretty psyched to learn that Rust also has some snack-stealing capabilities, all wrapped up in the seemingly-innocent semicolon. "What??", you must be thinking. "How can one small and often pretentious character be responsible for eating so much?" Well, that's what people say about me, and those people are fools. Let's learn!

![](/images/snacking.gif)

First off, I want to mention that if you're used to something like JavaScript, you're in for a headache. The only correct answer to "When do you used a semicolon in Javascript?" is a whispered *"No one knows."* So if you are coming to Rust from a chaos-type language, you might get a lot of unanticipated errors when compiling Rust.

I think this [Stack Overflow answer](https://stackoverflow.com/questions/26665471/are-semicolons-optional-in-rust) sums things up pretty well. "Almost everything in Rust is an expression. An expression is something that returns a value. If you put a semicolon you are suppressing the result of this expression, which in most cases is what you want."

Semicolons are used sometimes, and that sometimes is very important because they determine who gets to have a snack: you or the semicolon.

Most of the time, you use semicolons in a way you might expect. They help you tell the compiler that you are ready to do a thing.

But it's important to remember that expressions return a value and statements don't. The exception is that blocks are expressions but they should NOT have a semicolon follow them. If they do, all their hard work will get snacked right up. 

[Here](https://play.rust-lang.org/?gist=6a9620d9f8355046b0cbeeed2a206aa7&version=stable) is a working example of everything below if you want to test compiling and playing around!

So if you just want to get a snack from a function (or even outside of a function), you can just do this:

```
// Gives you your snack
fn getting_fed()  {
    let s = "apple";
    println!("Can't wait to eat this {}!!!", s);
}
```

You can also do something more complex, which might involve creating a `match` block or some other kind of block that checks for errors or certain kinds of data being input, signified by these curly brackets `{}`.

```
// Also gives you your snack
fn getting_hungry() {
    let s = {
        if 1 > 0 {
            "pear"
        } else {
            "no pear"
        }
    };
    println!("Can't wait to eat this {}!!!", s);
}
```

But what if you stick a semicolon in there because you just wanna play it safe and you have a lot going on?
```
// Gives NO SNAX
fn getting_starving(){
    let s = {
        if 1 > 0 {
            "banana"
        } else {
            "no banana"
        };  // this semicolon here is hella hungry!  
    };
    println!("Can't wait to eat this {:?}!!!", s);
}
```

NO SNAX!!! The semicolon will just eat it up and leave none for you! Extremely rude and also extremely sneaky, because unlike most other things, this manages to slip past the rigid compiler and cause confusion. So be careful out there, and watch out for hungry semicolons!

