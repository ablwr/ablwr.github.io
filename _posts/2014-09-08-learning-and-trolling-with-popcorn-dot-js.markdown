---
layout: post
title: "Learning (and trolling) with Popcorn.js"
date: 2014-09-08 11:01:02 -0400
tags: [small projects, flatiron]
---

Basically, I have a history of taking jokes too far. See also: [Tattoos of Avi’s face](http://instagram.com/p/ruP0rHjtbO/?modal=true). So when I was exploring [Mozilla](https://www.mozilla.org/)’s [Popcorn.js](http://popcornjs.org) and missing my Flatiron peers, I coded up a small app that would help me learn how to use Popcorn.js aaaaaaaand also troll my friends.

At Flatiron, we used a shared playlist system called [Sonos](http://sonos.com). Everyone could add tracks from online music collections like Spotify, Hype Machine, or Songza. Near the last third of the semester, as we were all on the brink of insanity and exhaustion, one song in particular kept making a rude appearance. I don’t know who started it or why, but the entire Flatiron office had to suffer through many, many, many instances of Seal’s Kiss from a Rose.

After Flatiron graduation, I was pretty excited to dig into some new projects while on the job hunt, but really missed hanging out with all of my Flatiron buds. To alleviate my withdrawl symptoms, I decided to integrate my Popcorn.js learning into an app to basically troll everyone I know.

To troll successfully, though, I first had to troll myself. Because music videos on youtube don't come with subtitles, I had to make those subtitles happen manually. I once had a job transcribing interviews, so I'm pretty fast. But to get the timing right, I still had to submit myself to many, many listens of the same song. 

Popcorn.js makes it easy to add supplemental media to video files based on timing.

Within a document listener, you create an instance variable with the .youtube suffix (obviously it's different if you are not using the YouTube API to access a video, but for this example, I used YouTube) and then declare a landing div ID and a link to the video itself.

```javascript

   var pop = Popcorn.youtube(
     '#video',
     'https://www.youtube.com/watch?v=i4tTnIimi8E' );

```

Afterwards, it's time to start adding footnotes! This takes in four options -- a start time (in seconds), an end time (also in seconds, big surprise), the text you want to display, and the target div. The application of subtitle footnotes is simple, but it's easy to see what kind of complex and interesting things can be done based on video playback times.

```javascript

   .footnote({
      start: 94,
      end: 97,
      text: "Won't you tell me is that healthy, baby?",
      target: "footnotediv"
   })

```

 At the end, just trigger play.

```javascript

    pop.play();

```

Try it yourself! [Sing your heart out here](http://ablwr.github.io/flatiron-karaoke).

There's also an easter egg, but you have to patiently wait for it (or sing sing sing for it).

User feedback: It worked! Everyone typed in a song and got Seal back and tried it again because they thought it was a bug. NOPE. The only person that didn’t get trolled had preemptively trolled by searching for “Kiss from a Rose” so she didn’t know it was the only possible song that could be returned.

In the future, I’d like to spend more time trying to figure out how a real karaoke app could be created by automatically generating accurate subtitles. I’d also like to spend more time on the CSS styles so I could figure out how to fake the text highlighting on karaoke videos. As I mentioned earlier, there's an easter egg -- I'd like to work on incorporating more complex supplemental data alongside video files, such as Google maps, Wikipedia page load triggers, and images.