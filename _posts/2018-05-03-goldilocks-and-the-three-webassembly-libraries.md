---
layout: post
title: "The Story of Goldilocks and the Three WebAssembly Libraries"
date: 2018-05-03
tags: [recurse center, webdev]
---

# 💁 🐻 🍨 🐻 🍨 🐻 🍨 🙆

I've had some starts-and-stops trying to learn Rust and also learn WebAssembly and work with chaos-language JavaScript. Everything's quite new, so I have been trying to find something that is not out of date, but also not too new that the features aren't quite where I need them to be yet, which is stable enough to perform basic operations and be sure that the problem is not just me. So I went on a journey to find some good-tasting WASM to add to my emerging web stack.

## She tasted the porridge from the first bowl.

First up was vanilla passing of Rust into WebAssembly and out into JavaScript. [Here](https://github.com/rust-lang-nursery/rust-wasm/blob/master/src/hello-world.md) is the "hello world" example. 

To implement, add `crate-type = ["cdylib"]` to your `Cargo.toml` and pass things from Rust (or the language of choice) to be compiled down into WebAssembly. From there, JavaScript can take care of the rest.

```
      fetch('hello_world.gc.opt.wasm')
        .then(r => r.arrayBuffer())
        .then(r => WebAssembly.instantiate(r))
        .then(wasm_module => {
            alert(`2 + 1 = ${wasm_module.instance.exports.add_one(2)}`);
        });
```

Code going into JS-land has to be preceded with `#[no_mangle]` as a way to let the WASM compiler know that it shouldn't do optimization on the function name and take it away, because it will be how we grab things up on the other side. It is the connecting key.

This wasn't bad, but involves a lot of code and a lot of JavaScript/client-side work, and I want to be working in and with Rust more than working in and with JavaScript to do the data processing aspects of my small project. Right now, this method is just a little too much for me and my goals (which are primarily self-education-based -- I already know JavaScript and I want to know Rust).

## "This porridge is too hot!" she exclaimed. So, she tasted the porridge from the second bowl.

Next up was `wasm-bindgen`. 

As much as I wanted to love this library, it seems like it hasn't quite warmed up enough yet. It is very new and very in-progress. Some of the features I was trying to work with were less than a month old.

`CompileError: wasm validation error: at offset 4: failed to match magic number`

I got a lot of compiler errors, but that's okay. I can work with that. That's basically the life of a Rust developer. It did take a very long time to compile, though, in my opinion, relative to other options. In addition to that, the code was very verbose on both the Rust side and the JavaScript side of things. [Here](https://hacks.mozilla.org/2018/04/javascript-to-rust-and-back-again-a-wasm-bindgen-tale/) is an introduction with a "Hello, World" example.

Getting things compiled was a little clumsy and verbose, which wasn't dissimilar to the initial method. 

Here's what it looks like:

First time, Rust Side:  
`rustup target add wasm32-unknown-unknown --toolchain nightly`  
`cargo install wasm-bindgen-cli`  

First time, JS Side:

`npm build`  

Regularly, Rust Side:
`cargo +nightly build --target wasm32-unknown-unknown`  
`wasm-bindgen target/wasm32-unknown-unknown/debug/planets.wasm --out-dir .`  

Regularly, JS Side:
`npm run serve`  

Not to mention having package.json, webpack.config.json, index.js, index.html, src/lib.rs, cargo.toml, and a whole lot of target files I don't understand or know about living both in the root of my directory as well as in the /target folder. It was hella messy!

It seems that only numbers and some strings can be passed through with this library. I was trying to send a tuple over. That wasn't a dealbreaker though, I could switch it up and send over less or differently-structured data. But sending over what seemed to be basically one function, I ran into this WASM error:

```
Module parse failed: WasmCompile: Compiling wasm function #10:astro::planet::heliocent_coords::hf02f7569fc4b7284 failed: local count too large @+24251
You may need an appropriate loader to handle this file type.
```

Too large? It's a floating integer with room for up to sixty-four bits! I could have kept at that, but thanks to the aptly-timed weekly Rust Study Group at Recurse Center, I was informed of some new libraries to try (thanks x100 to [Casey](https://github.com/casey) as always), so I hopped away again to try something else.

## "This porridge is too cold," she said. So, she tasted the last bowl of porridge.

Introducing `stdweb` (and `cargo-web`). 

Right away, the command line steps-to-get-things-done are much more elegant:

```
cargo web start --target=wasm32-unknown-unknown
```

This takes care of all the Rust and compiling and WASM and compiling and JavaScript and compiling for me. 

The examples are [ample](https://github.com/koute/stdweb/tree/master/examples) and diverse, including [canvas integration](https://github.com/koute/stdweb/tree/master/examples/canvas) and even an [NES emulator](https://github.com/koute/pinky/tree/master/pinky-web) on top of simple "hello worlds" like sending an alert to JavaScript and making a TodoMVP.  

The instructions and examples also offer implicit cleanliness in the file tree structure: Put your Rust in SRC, put your JavaScript in Static, and build only what you need.

## "Ahhh, this porridge is just right," she said happily and she ate it all up.

I haven't spent too much time finding headaches when working with `stdweb` instead of other libraries for getting Rust into the browser, but for now I am extremely satisfied. For me, this library is just right.

Got some WebAssembly tips? [Lemme know](https://twitter.com/ablwr) and thanks for reading!