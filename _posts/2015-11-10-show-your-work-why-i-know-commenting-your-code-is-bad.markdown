---
layout: post
title: "Guest post: Show Your Work: Why I know commenting your code is bad"
date: 2015-11-10 00:22:31 -0500
comments: true
categories: guest, programming
---

I've been kinda bad at blogging. I have a new job and some old jobs and lots of things that keep me from introspecting on code and archives. Fortunately I have great friends, and one of those friends is Kathryn Gronsbell, who reached out to me as an emerging developer (whether she thinks so or not) and wanted to write a *guest blog post*! As for me, a person who has very recently had to take on the codebase of at least five web complex and non-similar applications at my job... I can appreciate some good commenting. Commented-OUT code, on the other hand...

# Show Your Work: Why I know commenting your code is bad, but I do it anyway.
### Kathryn Gronsbell
### 2015-11-05

I like to ship ugly, early, and often. My challenge is I’m a Kathryn* who is in the middle of doing three very critical things:

1. Learning enough Python and Bash to be functional (and dangerous)
2. Building small scripts to expedite digitized asset quality control at my organization
3. Trying to triangulate how and why certain decisions were made and performed before my arrival, and how to understand, fix/reverse, or move forward (see Steps 1 and 2)

In 2013, Peter Vogel explained why “people” should not document or comment their code [[1]](https://visualstudiomagazine.com/articles/2013/07/26/why-commenting-code-is-still-bad.aspx). Vogel makes well-executed arguments, steeped both in conceptual logic and pragmatism.

“Some readers suggested that comments provided insight into what previous programmers thought their code was doing. I don't care what those programmers thought their code was doing -- I only care what their code actually does (though I do care why the previous programmers thought the code was necessary).”

I agree with Vogel here, on all points. But, I do care what the previous person thought their code was doing because it can help explain OTHER decisions that are not documented in the code (or anywhere else). And because my code is wobbly, like a baby deer that snuck into a moonshine distillery, I feel the need to add comments and leave some less elegant code commented-out so I can understand how a certain chunk came together. 

Example: 

```python
#This loops through the files and sets a variable “bambi” for the extracted string. This takes the legacy strings which are all uppercase and makes them lowercase alphanumeric strings so that they validate against the strings we create locally.
    for key in forest_fileDict:
        bambi = forest_fileDict[str(key)].lower()
        # bambi = bambi.lower()
```

It works, for me and for now. When it doesn’t work anymore I won’t do it anymore. Vogel’s argument about resource-intensity of code commenting reads true, but it also doesn’t apply to my current situation. Describing what the code does helps me learn (because I wrote it and had someone else verify it was accurate). I yearn for the day I can write something that is both self-describing and that I can read in 3 weeks and understand. Until then, I will crawl along with my #-prefaced nuggets of wisdom - and happily share my MacGyver’ed efforts for review and revision.

If I listened to this ideal practice, I wouldn’t be creating the processes I need to do my job because it would be too big of an obstacle to take on for every little process I needed done. The code will be ugly, but it will work. And that’s what we should aim for - an agile approach to learning and making. Imperfect action is better than perfect inaction.

I hope if you’re in a similar spot, you now know that you have a comrade. And that one day you, too, can be a “people” Vogel is talking to. 

\* Being a Kathryn does not involve being a real programmer or code guru. Being a Kathryn means spending hours on StackOverflow, sending over-explanatory email pleas to our very patient IT support folks, and constantly chatting friends about why my nested dictionaries aren’t printing as expected. And thanking very smart co-workers for helping crack uncrackable nuts.
