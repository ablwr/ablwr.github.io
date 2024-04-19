---
layout: post
title: "Researching file formats 34: iOS App Store Package"
date: 2024-04-19 08:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [IPA](https://www.loc.gov/preservation/digital/formats/fdd/fdd000593.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

Like last week's post on the Android package, the iOS App Store Package is also... (dun dun dun)... just a ZIP archive file!

It's also not really well-disclosed, with no official docs from Apple that specify the .ipa file as a format.

Structured like this:

- iTunesArtwork (this is just a png file without the extension)
- iTunesMetadata.plist (metadataaaaa)
- Payload/ (the app binary)
- META-INF/ (more metadatatatatata)

According to this [Apple documentation](https://web.archive.org/web/20181026175002/https://developer.apple.com/library/archive/qa/qa1795/_index.html) initially created at 2014-03-06, there are several types of .ipa files, which I'll summarize:
- App Store submission .ipa: "a compressed directory containing the app bundle and additional resources needed for App Store services, such as .dSYM files for crash reporting and asset packs for On Demand Resources"
- universal .ipa: "compressed app bundle that contains all of the resources to run the app on any device. Bitcode has been recompiled, and additional resources needed by the App Store, such as .dSYM files and On Demand Resources, are removed. For App Store apps, this .ipa is downloaded to devices running iOS 8 or earlier"
- thinned .ipa: "a compressed app bundle that contains only the resources needed to run the app on a specific device. Bitcode has been recompiled, and additional resources needed by the App Store, such as .dSYM files and On Demand Resources, are removed. For App Store apps, this .ipa is downloaded to devices running iOS 9 or later."
- universal app bundle: "the decompressed universal .ipa"
- thinned app bundle: "the decompressed thinned .ipa"

LC's Recommended Format Statement defines this as a ["distribution file"](https://www.loc.gov/preservation/resources/rfs/software-videogames.html), stating "Distribution file (e.g. ipa [Mac iOS], apk [Android], exe [Windows]): The distribution file is disseminated for public use regardless of the means of dissemination (on physical media or via an online source) and is comprised of one or more files from the gold standard build.

We all know Apple loves the "technical protections considerations" category, so this is a can-o-worms. There's [FairPlay](https://nicolo.dev/en/blog/fairplay-apple-obfuscation/), and the way it works out is a bit interesting, but I'm not going to get into it here -- I yawned while typing that, so I guess I'm lying about it being interesting, I was just using a generic word to describe it when I didn't have anything noteworthy!