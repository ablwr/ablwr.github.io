---
layout: post
title: "Rust Study Group Notes"
date: 2018-04-27
tags: [recurse center, rust]
---

*Editors note: Something I love so much about Recurse Center is the amazing, interesting, knowledgeable people in this space. I initiated a study group to learn more about Rust and here are the notes from the first gathering. Meta-note, this is more for our benefit than for yours, the general public, but I hope it may be useful for casual browsers, potentially, so I am posting a modified version here instead of purely in a private document.*


- Around the room everyone mentions what they want to get out of this study group. 

**Casey tips!** Community is really great for Rust, lots of good community standards about not being an ass. The IRC channel is really good, Mozilla runs it at irc.mozilla.org and there's #rust and #rust-beginners. The reddit is surprisingly good, at [/r/rust](http://reddit.com/r/rust).

## What should we do?:
Can we bring in what we learned, maybe a few minutes about what we learned or what we built. Or presenting.
Some things that are particularly hard like borrowing, mutability, types/strings.

Good small projects for beginners: 
- Anything small CLI using `clap`, or writing `tree`.
- Beginning: Read [The Book](https://doc.rust-lang.org/book/second-edition/), C++ `coreutils` have been re-written and are worth looking at.
- Stan notes that the Rust compiler has taught him a lot about C/C++ because it sorts out problems for you.
- https://play.rust-lang.org/ 

- Around the room everyone mentions what they are working on.

- `rustup` getting your rust versions, `cargo` is package management (no concept of workspace like $GOPATH), `rustc` calling rust (like `rustc -v` for version)

- `clippy` can help give you hints, it's like a linter with extra suggestions.

**Question: What are the downsides?**
- There are like 8 types of strings that you have to be specific about. It's nice for handling weird edge cases but sometimes you have to do weird type conversions that you wouldn't have to do in other languages.
- The strictness in borrowing/mutability causes patterns that are easy in some languages are very difficult in rough. Like making a graph, the nodes don't get garbage-collected if there are outstanding references, but in Rust by default because it doesn't want to add any overhead for heap allocation, and don't want to reference a node no longer around, it's not possible to write it without adding an additional ref-counting wrapper.
- In Rust, it needs to guarantee no two things are mutating the same thing
- Having to tell it what you want to copy.
- You can pass a ref of a string into a function but you can't pass it out. You can't return a reference (potentially) without telling it how long it will live for.

**Learning time**  
Talking about: Owned data, borrowed data. Owned, you have access to it and its around as long as you keep it around. Nothing someone else can do will take that data away. Borrowed data is a reference owned by someone else, so you can't store it to a variable and access it later, because the owned source might later go away. This manifests in strings. The two main types are `String` (owned data) and `&str` (borrowed data). Probably a reference to a string owned elsewhere.

Why can't I return a string from a function? is a popular newbie problem, so lets answer it.

Goal: take a string, append a character to it, return that new character.

```
fn main() {

  fn foo(s: &str) -> &str {
    let new_string = String::from(s);
    new_string.push_str("foo");
    return &new_string
  }

}
```

So this above code won't work because it is trying to modify something that is borrowed.

Note: return statements are optional, usually.

```
fn main() {

  fn mutate_foo(s: &str) -> String {
    let mut new_string = String::from(s);
    new_string.push_str("foo");
    return new_string;
  }

}
```
This returns an owned `String`, and instead of returning a reference to the owned `String`, it returns a new `String`. We are allocating the string and instead of returning a borrow into the data, we return the data itself.

Function is going to return new_string, a `String` type.
When main returns, S will go out of scope and the data will be released.

`PathBuf` is an owned path, and `&Path` is a reference to a borrowed path.

The compiler will magically insert drop functions that gets rid of resources, like memory deallocation or file/databases closing. The compiler inserts these automatically.

Question: Does Rust have a Classes-type construct like Python? A: Structs  

```
struct Foo {
  s: String
}
```

More abstract class:

```
struct File {
  n: u64
}
```

The Rust drop function doesn't know this is a file so it won't do anything special for cleaning up. `Drop` is on a `Trait` called drop though...

```
impl Drop for File {
  fn drop(self){
    // do whatever to close self
  }
}
```

Question: Is Trait like an Interface in Go? Yes.

```
trait Clickable {
  fn on_click(&self);
}

struct Button {
  message: String,
}

impl Clickable for Button {
  fn on_click(&self){
    println!("{}", self.message)
  }
}

impl Button {
  fn change_message(&mut self, m: String) {
    self.message
  }
}
let b = Button{message: "hello".to_string};
b.change_message("bye".to_string);
```

A Trait is usually a function with no body inside because it just describes how something CAN be used but doesn't implement it.

The purpose of Traits is so that you can have a consistent interface without having to care about the specific kind of object. 

Talking through some fav Traits:  

`Sync`: if a type has sync on it, it means it is safe to share between threads. If you try to share between data and the class doesn't have this implemented, the compiler will complain if you try to send it over to another thread. But most of the time it gets implemented for you by the compiler.

`AsRef`: Allows you to cheaply convert to a reference to something else, like string to bytes. `&str` implements `AsRef([u8])` so if you have access to the str, you can cheaply get access to the bytes it contains.



