---
layout: post
title: "Researching file formats 33: Android Package"
date: 2024-04-12 08:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

First off, this work was made incredibly easier thanks to the work of Johan van der Knijff, particularly the blog series around working with mobile apps, the latest being ["Towards a preservation workflow for mobile apps"](https://www.bitsgalore.org/2021/02/24/towards-a-preservation-workflow-for-mobile-apps) from 2021, but the older posts on Android specifically hold up well and have been very helpful, too.

This format was somewhat easy because it's secretly a ZIP archive file. Even more, it's very similar to being a Java JAR file. There are just specific structures that make it an APK file instead, because that's what systems that read APK files will expect. Some folders, some XML files, and that's about it.

If you unzip it, you'll see:

- META-INF/: Directory that contains the manifest file, signature, and a list of resources in the archive
- lib/: Directory containing compiled code related to specific platforms
- res/: Directory containing non-compiled resources (e.g. images)
- assets/: Directory containing applications assets
- androidManifest.xml: name, versioning information and contents of the APK file
- classes.dex: Compiled Java classes that can be run on Dalvik virtual machine and by the Android Runtime
- resources.arsc: Compiled resources file such as strings

Even though the format is "easy", there's still issues given that there's no real official specification, there's just some [guidance from Google](https://developer.android.com/guide/components/fundamentals) and digging around in the code itself, making it easy enough to understand but a little harder to solidly prove (an endless battle with this project!).

The licensing stuff between Google and the Android open source project is a little hairy to explain succinctly, too. There's also some stuff to consider around "technical protection considerations" and encryption / privacy / DRM, making things "safe", everything on that topic can be challenging. There's application signing, authentication, and regular encryption in addition to other under-the-surface complications with the "Google Play Store." Next week I'll cover a format that knows even more about that stuff, the iOS App Store Package.