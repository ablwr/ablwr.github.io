---
layout: post
title: "Considering Rust"
date: 2018-04-09
---

I am now in an informal Iron Blogging challenge with [Janice](https://contrepoint.github.io/recurse-center-starts-to-feel-like-home) and [Marianne](http://mkcor.github.io/2018/04/09/week-2-day-1-at-rc.html) in my Recurse Center batch, so I must talk about technical things and personal things and opinionated things, and NOT BE AFRAID!! This is a blog post ramping up to something more technical and more opinionated.

Last Saturday, I paired with [Casey](https://github.com/casey), who helped me build something in Rust, a language that I've admired from afar (and wow, I saw a talk from Steve Klabnik about Rust over 4 years ago, when both me and the language were still code toddlers -- okay, mostly me) but haven't actually looked at (too many bouncing around the many many languages I had to write at previous places of work for a cool new one). Casey did an amazing job at explaining everything extremely well (and extremely patiently) and I was (and am) feeling super 💪 pumped about RUST. 

Here is what "we" wrote, in its entirety:

```
extern crate image;

use image::GenericImage;
use image::RgbaImage;
use std::fs::read_dir;
use std::path::PathBuf;
use std::path::Path;

struct ImageSequence {
  images: Vec<RgbaImage>,
}

impl ImageSequence {
  fn from_dir<P: AsRef<Path>>(dir: P) -> ImageSequence {

    let mut images = Vec::new();

    for dir_entry_result in read_dir(dir).expect("failed to read data/mandelbrot") {
      let dir_entry = dir_entry_result.expect("failed to unwrap dir entry");
      let path = dir_entry.path();
      println!("{:?}", path);
      let img = image::open(path).expect("failed to decode image");
      println!("{:?}", img.dimensions());
      println!("{:?}", img.color());
      images.push(img.to_rgba());
    }

    ImageSequence {
      images: images,
    }
  }
}


fn main() {

  let dir = PathBuf::from("data/mandelbrot/");
  let mut seq = ImageSequence::from_dir(dir);

  for (i, image) in seq.images.iter_mut().enumerate() {
    for pixel in image.pixels_mut() {
      pixel.data[0] = 0;
      pixel.data[1] = 0;
    }
    println!("manipulated this image {:?}", i)
  }

  for (i, image) in seq.images.iter().enumerate() {
    image.save(format!("data/out/{}.png", i)).expect("failed to save");
    println!("successfully saved image # {:?}", i)
  }

}
```

Wow, so beautiful! This takes a series of images of a fractal that I generated (`ffmpeg -f lavfi -i mandelbrot=size=640x480:rate=24 -c:v libx264 -t 5 mandelbrot.mkv`) and split into images (`ffmpeg -i mandelbrot.mkv img%04d.png`) and loops through each pixel in each image and manipulates it in some way (the above reduces the red and green to black, leaving only the blue channel), and saves them all in a new directory. Everything made sense to me and everything looks and works great. I need to go in and optimize things (like a .DS_Store will throw this entire thing off right now), but pretty good for a few hours of instruction.

Well, today's Monday and I'm stubbornly back to working solo and here is an approximation of what my code is looking life so far today, working on the simple? task of writing a Universal Turing Machine ala [Destroy All Software](https://www.destroyallsoftware.com/screencasts/catalog/computing-by-changing):

```
fjdksafjlkds;fjk;dasj 
fdjasklfjlds;;
fdakjslf;dsfjkad;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
~~~~~~~~~~~~~
errro errrrr errrrororrr
undeclared lifetime
expected lifetime parameter
abort
cannot compile ever!
``` 

So, I have a lot more work to do on my own getting up to speed on this language, but I'm overall really happy with it! (Also I did resolve these lifetime errors but they were funnier than some of the others that came my way.) Over the weekend, I listened to one of my favorite people [Lee Baillie on the New Rustacean podcast](https://newrustacean.com/show_notes/interview/irr_2017/lee_baillie/index.html) (which is great so far, I am gonna listen to them all, and also I love that the website is also built rust docs style). Anyway, Lee describes the difference betwen Rust and Ruby (a language I learned right alongside Lee 4 years ago!!) as parenting styles, the stern parent and the go-do-whatever parent. Anyway, they explain it better than I am at summarizing it, but after years of loosy-goosy Ruby, I'm ready for some structure from the compiler, letting me know up front that it is not about to put up with all my bullshit.

As you, reader, may or may not know, my ambitious project during my time on this sabbatical is to build a video codec (despite knowing less math than the average American, which is already quite low, and not knowing C, and some other things that are likely important), and I have more to say about that, but I like to keep my blog posts short-n-sweet.

