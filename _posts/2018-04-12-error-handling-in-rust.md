---
layout: post
title: "Error handling in Rust"
date: 2018-04-12
tags: [recurse center, rust]
---

I've been working my way through [rustlings](https://github.com/carols10cents/rustlings), which is a great great resource and I highly recommend it for getting started with Rust. I especially like it because it forces me to read chapters of the excellent [Rust Programming Language book](https://doc.rust-lang.org/book/second-edition/ch01-00-introduction.html) piece-by-piece and then put the chapters into practice with tiny exercises in the [sandbox](https://play.rust-lang.org/). This is great for me because I am very impatient, especially with myself and my own learning (seriously I listen to podcasts at 2x speed and can't handle normal-speed anymore because I'm like "get to the goddamn point!"), and this pushes me to sit down and read things in specific chunks and test my reading comprehension, which can also be not-great when I'm trying to rush through things.

Going through the rustlings tutorials though, I got really stuck on error handling. Error handling is important, so there are a lot of different ways to handle errors in Rust! The good news is you don't end up with an `undefined` important thing or have to fill your codebase with checks for variable presence. The compiler won't compile unless you have all of that handled.

What are the different ways you can deal with this by preventing it?

## `panic!`

If something should actually cause everything to break if it reaches this point, [panic!](https://doc.rust-lang.org/std/macro.panic.html) is a macro that can summon that chaos.

## `.unwrap()` and `.expect()`

`.unwrap()` is cool but it will throw an error if it doesn't know what to do. It'll just panic, which is not cool. And `.expect` is similar but you can put a message in the parens so you'll have a better idea as to what happened and what went wrong. 

If you want to be a little more advanced, you can do some matching:

## Results: `Ok` and `Err` 

This is like Rust's version of "try/catch" and it goes something like this: 

```
match this_thing {
  Ok(thing) => thing,
  Err(e) => return Err(e),
};
```

When using it inside of a function, the function needs to define the type as `Result`, and that result needs two types inside.

But a shorter version of this can just be `this_thing.ok()` or `this_thing.err()` to get just one of those.

This kind of checking can also be done with boolean returns, using `.is_ok()` or `.is_err()`, which is handy and less verbose.

## Options: `Some` and `None` 

Instead, if want to return something, and if that something isn't right, return something that is a nothing -- do you see how this is confusing? What I mean is if you want to definitely respond with what you intend to have a function return and if that doesn't work, return `None` and then you can handle that accordingly but it won't fail to compile. 

This seems less common in its long form because it is verbose, and some things handle errors like this more succinctly.


## `.unwrap_or()`... `.unwrap_or_else()`!!

This is a handy way of dealing with results, which is like "unwrap this, or if that can't happen, give me something else as a backup."

There's also the more dramatic `.unwrap_or_else()` where inside the parens you can pass in a function or something.

## Errors when writing errors

Kinda like when I was trying to work in C and then trying to debug a problem, I keep having meta-problems stir up, and that is going to be true with Rust as well. My error messages keep giving me error messages! 

An error that I kept getting was ["mismatched types"](https://doc.rust-lang.org/error-index.html#E0308), like this:

```
   = note: expected type `std::result::Result<std::string::String, std::string::String>`
              found type `std::option::Option<std::string::String>`
```

Since I'm coming from high-level-language land, I'm not used to having to declare-in-advance and continue to worry about what type something is. So since I'm learning this at the same time as learning about these kinds of error handling and also concepts of borrowing, it was hard for me to do a deep reading of compile error mostly because I'm an impatient fool, but also because of this confusion (or I will at least push this as the scapegoat). But again with the help of a patient fellow RC-er who can manage to very politely tell me to actually read the error messages repeatedly, I now know that I was sending something that the compiler correctly identified as an `Option` type while also simultaneously telling it that it should be receiving a `Result` type. It was just saying "Hey man, you told me you were sending over some pizza, but this is a head of lettuce, what the hell?"

Am I wrong about this stuff? Please let me know so I can make a correction! Thanks!
