---
layout: post
title: "Using videogrep to make supercuts"
date: 2014-07-22 22:36:12 -0400
tags: [small projects, video, flatiron]
---

[Videogrep](https://github.com/antiboredom/videogrep) is a Python-based application that searches through a video file using its subtitles track and can cut video clips based on its search criteria.

Videogrep is SUPER easy to use... as long as ffmpeg is installed properly. If not, prepare for some configuring and installing. 

I used videogrep to search through one of my favorite movies, Terrorvision, to find every time a character refers to something as "The Pleasure (noun)." Hint: it happens more times than you would think.

To do this, I only had to type one line and videogrep did the rest of the work.

`python videogrep.py -i Terrorvision/Terrorvision.avi -o test_video.mp4 --search 'Pleasure' `

It searched through the subtitles file and found six instances, which it printed to the screen along with their timestamps.

```
524.357 to 527.86:  Pleasure Palace, here we come.
1660.284 to 1663.453: Otherwise known as the Pleasure Zone.
1734.4 to 1736.651: The Pleasure Den.
1776.859 to 1779.527: on to the Pleasure Dome.
1779.528 to 1782.905: To the Pleasure Dome.
1840.756 to 1842.548: The Pleasure Dome.
```
If there is an error, at this point it will let you know. But if all goes well, the following will print to the screen:

`Your video is ready ! Fingers crossed for the Oscars !`

Here is the video supercut. Something that might have taken a few hours for me to piece together using my memory of the movie and video editing software was done in less than a minute using the powers of Python and FFMpeg.

Voila!

<iframe src="//player.vimeo.com/video/99057389" width="500" height="282" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe> <p><a href="http://vimeo.com/99057389">Pleasure Supercut</a> from <a href="http://vimeo.com/orangelazarus">Ashley Blewer</a> on <a href="https://vimeo.com">Vimeo</a>.</p>


This was just a simple example, but videogrep can get more specific based on the regular expression added into the search string. In the above example, I knew "Pleasure" was a proper noun because its the name of many rooms in the Putterman household. If I really wanted to grab every instance of the word, I would have had to search for 'pleasure|Pleasure' to capture both uppercase and lowercase.

Videogrep can be even more powerful because it understands [pattern recognition using pattern search](http://www.clips.ua.ac.be/pages/pattern-search). I was able to extract what I wanted by just typing in one word, but it also understands word patterns. For example, you can use flags like JJ for adjective or NN for noun and it will extract every instance of a particular speech pattern.

It can also search for hypernyms, which are words that fit into a certain category and have a semantic relation to each other. For example, if you searched for automobile, you might also want to extract similar words like car, truck, or van. If you weren't picky about what kind of bird you were looking for, a hypernym search would result in crows, seagulls, and eagles. 

Enjoy using videogrep and watch out for the monster!

<iframe src="//player.vimeo.com/video/99093635" width="500" height="282" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe> <p><a href="http://vimeo.com/99093635">TerrorVision Monster</a> from <a href="http://vimeo.com/orangelazarus">Ashley Blewer</a> on <a href="https://vimeo.com">Vimeo</a>.</p>
