---
layout: post
title: "Researching file formats 19: Java class file"
date: 2024-01-05 09:00:00 -0500
tags: [file formats, fdds]
---

Java configuration class file format.

Might be candidate for least appealing documentation/specification (legacy, [here](https://web.archive.org/web/20190203163541/https://docs.oracle.com/javase/specs/jvms/se7/html/jvms-4.html).)

The hardest part of this format was having to explain the JVM in a way that makes sense for a website people primarily access to understand actual files they've come across in their preservation collections. Maybe I know too much? Maybe I know too little? It's a challenge to comprehensible cover a file that has the purpose of being strictly from going from one state to another. That _is_ a category within the SDF, ["Production phase"](https://www.loc.gov/preservation/digital/formats/fdd/fdd_explanation.shtml#identification): "Indication of how the format is generally used during the content life cycle, e.g., by creators or authors (initial state), by distributors, publishers, or archives (middle state), or as delivered to endusers (final state).". My draft research says something along the lines of: "This file is intermediary. It is derived from Java code, written as a file, and then executed by the Java Virtual Machine (JVM). It is used while working with Java, on the way to creating a useable, compiled format (like a .jar file). Not suitable as an archival format, nor particularly important to keep because it's just a middle file between .java (or other source) and .jar (or other target)." But to help someone understand all of that, there has to be some explanation of these types of programming languages, the reason they compile into a file, and then that's just on their way to being compiled into another file. Oh, and do it in an unbiased way, of course!

Java isn't my fav.

Also, a quick and apolitical summary of Sun Microsystems and Oracle?? Help! That can be a challenge, too!
