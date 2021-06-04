---
layout: post
title: "WebRTC lingo"
date: 2021-06-03 12:00:00 -0500
tags: [video, webdev]
---

A big problem with getting into video *in general* is all of the esoteric lingo that you have to learn, and WebRTC introduces a slew of new acronyms and words into the mix. Since WebRTC is basically a protocol composed of or built using many other protocols, it can turn into an acronym soup pretty quickly. It can make it difficult to even have a high-level conversation about live video streaming on the web without all of the shortcuts used to describe different components of the server infrastructure.

Something to know in general is that WebRTC is both a protocol and an API.

From *[WebRTC for the Curious](https://webrtcforthecurious.com/)*: "The WebRTC protocol is a set of rules for two WebRTC agents to negotiate bi-directional secure real-time communication. The WebRTC API then allows developers to use the WebRTC protocol. ... A similar relationship would be the one between HTTP and the Fetch API. WebRTC the protocol would be HTTP, and WebRTC the API would be the Fetch API."

[WebRTC the protocol](https://datatracker.ietf.org/wg/rtcweb/about/) (IETF) is not language-specific, it just lays out the rules that you need to follow, while [WebRTC the API](https://w3c.github.io/webrtc-pc/) (W3C) is JavaScript-specific.

The following definitions help contextualize certain acronyms within the context of WebRTC specifically, not meant to provide an overall, generalist definition for significant protocols (e.g. TCP, which is used for many things).

## DTLS 
#### (Datagram Transport Layer Security) 

DTLS (Datagram TLS) works in conjunction with [SRTP](#srtp) to allow for secure data exchange between two peers in the transport layer.

Standard: [IETF RFC 6347](https://datatracker.ietf.org/doc/html/rfc6347)

## ICE
#### (Interactive Connectivity Establishment)

This protocol establishes a [UDP](#udp) [NAT](#nat) connection between sessions using [STUN](#stun) and [TURN](#turn) -- maybe the peak of the acronym soup! Basically it arranges for most direct way that two computers to be able to talk directly with each other, like a matchmaking service.

Standard: [IETF RFC 5245](https://datatracker.ietf.org/doc/html/rfc5245)

## MCU
#### (Multipoint Conferencing Unit)

This network routing system allows clients to connect to multiple other clients in a session through a centralized architecture. I recommend looking at this [WebRTC Glossary](https://webrtcglossary.com/mcu/) entry for a short video explainer. This design is compared with mesh networking design or [SFU](#sfu). The MCU is also referred to or can be thought of the "mixer."

## NAT 
#### (Network Address Translation)

This is a widely used protocol that handles IP address mapping and routing. When you think about what your router does, allowing your computer to have a local and a public IP, that's the type of thing managed by NAT.

[STUN](#stun), [TURN](#turn), and [ICE](#ice), essential to managing WebRTC streams, are all built upon this protocol.

Standard: [IETF RFC 3022](https://datatracker.ietf.org/doc/html/rfc3022) (and multiple other standards cover or refine this protocol)

## NV 
#### (Next Version)
Used in the context of WebRTC NV, this is a future, optimized variant of the WebRTC collection of protocols (like a 2.0). I don't know that this really comes up in conversation that often and is perhaps being deprecated as a term now that WebRTC *has* hit 1.0, but it's something to be aware of. I'm not going to get into all the nuances of standards development, but things take a longer time than anyone would like and some people work past the spec while it is still being developed and people need to refer to future functionality that is still a bit of a ways off in terms of being accepted and implemented. 

## RTC 
#### (Real Time Communication)

This concept represents the area of study that is close-to-simultaneous-as-possible exchange of data, often multimedia. It's not a specific protocol or standard, just an acronym used to describe things that fit into this category. You can do this without the web.

## RTP 
#### (Real-time Transport Protocol)

This protocol delivers audio and video over IP networks, usually over [UTP](#utp). It's part of the Application layer (as opposed to Transport layer of the [internet protocol suite](https://en.wikipedia.org/wiki/Internet_protocol_suite)).

Standard: [IETF RFC 3350](https://datatracker.ietf.org/doc/html/rfc3350)


## SFU 
#### (Selective Forwarding Unit)

SFU is a routing system receives different audio and/or video streams and relays them to others on a call. Each client will send its video out but receive one-or-more streams back. [mediasoup](https://mediasoup.org) is a popular SFU framework.

## SCTP 
#### (Stream Control Transmission Protocol)

Transports data channels, and can support a lot of features that improve streaming quality, like multiplexing, flow control, and delivery performance improvements. Part of the Transport layer of the [internet protocol suite](https://en.wikipedia.org/wiki/Internet_protocol_suite).

Standard: [IETF RFC 4960](https://datatracker.ietf.org/doc/html/rfc4960)

## SDP 
#### (Session Description Protocol)

SDP describes audio and/or video sessions (announcement, invitation, etc). It only does description and doesn't manage any of the transport, like many of the other WebRTC protocols.

Standard: [IETF RFC 4566](https://datatracker.ietf.org/doc/html/rfc4566)

## SRTP 
#### (Secure Real-time Transport Protocol)

This protocol, Secure [RTP](#rtp), allows for the exchange of media via [UTP](#utp) working with [DTLS](#dtls) to provide a secure connection. 

Standard: [IETF RFC 3711](https://datatracker.ietf.org/doc/html/rfc3711)

## SSE 
#### (Server-Sent Events)
SSE is an API for opening an HTTP connection for receiving push notifications from a server in the form of DOM events" ([ref](https://www.w3.org/TR/eventsource/)).

Websockets are used to implement WebRTC [signaling](https://webrtcforthecurious.com/docs/02-signaling/). WebRTC signaling can use [WebSockets](#websocket), [SSE](#sse), or [XHR](#xhr)

Standard: [W3C Server-Sent Events Recommendation](https://www.w3.org/TR/eventsource/)

## STUN 
#### (Session Traversal Utilities for NAT)

This protocol helps to find the relevant public IP address behind a [NAT](#nat) server, used in conjunction with [TURN](#turn).

Standard: [IETF RFC 5389](https://datatracker.ietf.org/doc/html/rfc5389)

## TCP 
#### (Transmission Control Protocol)

TCP is one of the primary ways to access the internet (and the most common), with so much built on top of it (like the Web, email, file transfer, etc.). WebRTC implementations are more likely to use or default to using [UDP](#udp) instead of TCP, but TCP can and is used as well.

Standard: [IETF RFC 793](https://datatracker.ietf.org/doc/html/rfc793) (and more)

## TURN 
#### (Traversal Using Relay around NAT)

Used in conjunction with [STUN](#stun), this protocol arranges the server connections that allow for media to be exchanged between clients.

Standard: [IETF RFC 8656](https://datatracker.ietf.org/doc/html/rfc8656)


## UDP 
#### (User Datagram Protocol)

This is the default transfer protocol for streaming media between WebRTC peers.

Standard: [IETF RFC 768](https://datatracker.ietf.org/doc/html/rfc768)

## WebSocket

A protocol that allows for two-way direct, asynchronous communication between a client and host, working on top of the [TCP](#tcp) layer. There is an initial "handshake", and then messages (containing data) can flow between browsers and servers. 

Websockets are used to implement WebRTC [signaling](https://webrtcforthecurious.com/docs/02-signaling/). WebRTC signaling can use [WebSockets](#websocket), [SSE](#sse), or [XHR](#xhr)


Standard: [IETF RFC 6455](https://datatracker.ietf.org/doc/html/rfc6455)

## WebTransport

WebRTC's potential/alleged successor. There's a good overview and some opinions in [this blog post](https://bloggeek.me/webrtc-unbundling/) about potential plans for WebRTC "unbundling", as well as [this blog post](https://blog.bitsrc.io/will-webtransport-replace-webrtc-in-near-future-436c4f7f3484) if you want to know more about that.

## XHR 
#### (XMLHTTPRequest)

XHR is a standardized HTTP request protocol that can be used to implement WebRTC [signaling](https://webrtcforthecurious.com/docs/02-signaling/). WebRTC signaling can use [WebSockets](#websocket), [SSE](#sse), or [XHR](#xhr).

Standard: [WHATWG XMLHttpRequest](https://xhr.spec.whatwg.org/) Living Standard


## Bonus!

This brief summary of WebRTC terms took longer to compile than I anticipated -- there really is a lot going on here. Anyway, a few extra things that are not covered here:


#### A few other very short definitions

- AR/VR: Augmented reality / virtual reality
- E2EE: End to end encryption
- P2P: Peer to peer

#### Codecs

Not going to go into all of these, but some to specifically be aware of when working with WebRTC:

- AV1
- DTMF ("touch tone")
- HEVC
- Opus
- h264, h265
- VP8, VP9
- VVC
- 
####  Other resources
- [awesome-rtc](https://github.com/rtckit/awesome-rtc)
- [rtcweb](https://datatracker.ietf.org/wg/rtcweb/about/), IETF collection of protocols
- [WebRTC for the Curious](https://webrtcforthecurious.com/)
- [WebRTC 1.0: Real-Time Communication Between Browsers](https://w3c.github.io/webrtc-pc/), W3C JavaScript (technically ECMAScript) API
- [WebRTC Glossary](https://webrtcglossary.com/) - Everything I've covered and more!
- [I know X, what does WebRTC get me? - Sean DuBois | January 2021](https://www.youtube.com/watch?v=s4zBbyNgaMc)
