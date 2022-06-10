---
layout: post
title: "Aura reader for two"
date: 2022-06-09 20:00:00 -0500
tags: [divination, small projects, webdev]
---

This blog post starts with a contextual-maybe-philosophical overview and then goes into a technical overview for my [AURA READER... FOR TWO](https://github.com/ablwr/aura-reader-for-two)!

## The first part

![aura](/images/new-aura.jpg)

Two years ago, I made a a little [aura reader](https://bits.ashleyblewer.com/aura-reader-2020/), as part of an ongoing series I've been doing on-and-off around techno-divination and mysticism (the other two are [the i-ching](https://bits.ashleyblewer.com/i-ching/) and the [barthes-tarot](http://bits.ashleyblewer.com/barthes-tarot/)). I want to tackle tea-leaves next!

I haven't done a lot of little creative coding projects lately, but I've been wanting to update my aura reader for a while -- the implementation is super simple (I prefer to work on little projects that only take a few hours rather than getting stuck into something for months at a time).

I'm also interested a bit in forcing people to engage with tech-based projects in a way in which time plays a crucial factor (see also: [throttled](https://ashleyblewer.com/throttled.html), which is essentially a movie on the web because the server moves so slowly).

So the aura reader, I wanted it to be more interactive, inviting people to have to describe someone's aura to them and vice-versa, rather than the solo meditation of the original aura-reader (except when posting the results to twitter, which I regularly do, but I can't show you because my tweets auto-delete).


![aura](/images/orig-aura.jpg)

I thought I had written a blog post about the first aura reader, but I guess I hadn't! It was inspired by a trip to [Magic Jewelry NYC](https://www.magicjewelrynyc.com/aura-photo), every NYCrs favorite spot for getting an aura reading. During a pandemic, it was nice to be able to enjoy seeing your aura from the comfort of your own apartment.

Three years into a pandemic, it's still nice to be able to connect with people who are far away, either long-term or short-term.


![aura](/images/new-aura-2.jpg)

So again, this works a bit like a performance piece -- you have to already be in sync with the aura-reader partner because each room only lasts for 5 minutes. You have to make the session, invite your friend, and then both join and describe your auras to each other. You won't be able to see your own aura, just your little self in the corner of the screen.

## The second part

As the [README]() describes, I made this using [Daily](https://daily.co), [Next.js](https://nextjs.org), [TypeScript](https://www.typescriptlang.org/), [Tailwind](https://tailwindcss.com/).

I work at Daily, so that was a convenient choice! But it was super easy to get up-and-running, something I'm always telling people in a day-to-day work context. I started by testing with the Prebuilt "drop-these-two-lines-of-code-in-to-replace-Zoom/Meet" to start and then switched to doing everything in a custom way (something I also recommend).


I got to use the brand-new (seriously brand new when I started putting this together!) [daily-react-hooks](https://docs.daily.co/reference/daily-react-hooks#main), which made state management a lot easier. I'm not a React-head, so I'll take all the help I can get. Next.js and TypeScript helped with that.

This was my first time using Tailwind and I really got a lot out of it, it did feel intuitive to add the CSS I needed in the HTML instead of writing it all myself by hand.

The app is deployed on Vercel. I wanted to deploy it to GitHub Pages because I have a nice routing system that sends all of my projects to a subdomain of mine, but it just wasn't having it. I wasn't able to set up a GitHub Action at all, or any other hacky methods I've gotten away with in the past through manual builds. I don't know if the services was having problems or what (literally could not commit the action), but it was a one-click thing with Vercel. 

I had to almost totally rewrite the original code, which was fine because it was pretty sloppy to begin with. I cleaned it all up and moved it to TypeScript before realizing that you can't put lipstick on a pig or whatever the phrase is, because adding types didn't make up for some structural issues.

![aura](/images/aura-frown.jpg)

The biggest things I had to do were:
- make the video and aura take up more space
- work on mobile
- create rooms for two

Daily helped with all of those things, because it's managing any call infrastructure and just passing me a video stream to style as I like. I fully expect it to still be a bit wonky on mobile just because that's the reality of mobile devices (permissions settings plague me).

Styling to have everything fit on the screen and on top of each other was tricky/finicky, but I eventually got it to work and just with Tailwind. This is where I should go back and figure out exactly what made things click, but I'm a bit lazy.


Something that did help is that [`face-api`](https://justadudewhohacks.github.io/face-api.js/docs/index.html), which I used for the original aura-reader and I kept the exact same face models, has a very helpful resizing method for fitting the canvas on top of the video (which is taking up the full viewport):

```js
const canvas = document.getElementById('overlay') as HTMLCanvasElement

const displaySize = { width: window.innerWidth, height: window.innerHeight }
faceapi.matchDimensions(canvas, displaySize)

const resizedDetections = faceapi.resizeResults(detections, displaySize)

// x,y = size of video display
const x: number = resizedDetections.detection.box.x
const y: number = resizedDetections.detection.box.y
// w,h = size of face, in pixels
const w: number = resizedDetections.detection.box.width
const h: number = resizedDetections.detection.box.height
```

Daily helped with making new sessions, it's just a simple API call:

```js
const createRoom = async () => {
  try {
    const res = await fetch('/api/room', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
    })
    let resJson = await res.json()
    router.push(
      {
        pathname: `/sessions/${resJson.name}`,
        query: {
          url: resJson.url,
          room: resJson.name,
          exp: resJson.config?.exp,
        },
      },
      // This is to provide a cleaner URL
      `/sessions/${resJson.name}`
    )
  } catch (e) {
    setIsError(true)
  }
}
```

Because this only works with a maximum of two people, it's easy enough to handle the media elements:


```js
useDailyEvent(
  'track-started',
  useCallback((e) => {
    // Because each call has max 2 participants, there's only two places
    // where they can go: local in the corner, full screen for the partner
    if (e.participant.local) {
      let localVid = document.getElementById(`local`) as HTMLVideoElement
      localVid.srcObject = new MediaStream([e.participant.videoTrack])
    } else {
      let otherVid = document.getElementById(`other`) as HTMLVideoElement
      otherVid.srcObject = new MediaStream([e.participant.videoTrack])
      let otherAud = document.getElementById(`otherAud`) as HTMLAudioElement
      otherAud.srcObject = new MediaStream([e.participant.audioTrack])
    }
  }, [])
)
```

I can also rely on Daily to provide any error handling around the meeting -- such as when the meeting ends at 5minutes or if a third person tries to join the room and has to be told that the room is full:

```js
/*
  Take care of any errors, send guidance and clarity
*/

function raiseError(msg: any): void {
  if (msg.errorMsg) {
    // e.g. "Meeting is full", can handle more precisely later
    setErrorMsg(msg.errorMsg)
  }
}

useDailyEvent(
  'error',
  useCallback((ev) => {
    raiseError(ev)
  }, [])
)
```

Okay, those are some of my quick notes! Hope you [enjoy](https://aura-reader-for-two.vercel.app/) and please [let me know](https://github.com/ablwr/aura-reader-for-two) of any awkward bugs you find -- I'm sure there are PLENTY because I've barely tested it myself! 

![aura](/images/aura-mobile.jpg)

