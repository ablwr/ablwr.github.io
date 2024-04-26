---
layout: post
title: "Researching file formats 35: Apple ProRaw"
date: 2024-04-26 07:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [Apple ProRAW](https://www.loc.gov/preservation/digital/formats/fdd/fdd000594.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

This blog post from Lux on ["Understanding ProRaw"](https://www.lux.camera/understanding-proraw/) is useful not just in what it purports to do, but as an overall explainer for how digital cameras work these days. It's great! And it explains the format more thoroughly than I can or want to here.

This [publicity announcement from December 14, 2020](https://support.apple.com/en-us/HT211965) might be the closest thing we get to a specification from Apple:  (note that the bottom says September 28, 2022, but that's because it was edited later, marginally, so that can be ignored -- the 12/14/20 date came from the [wayback machine copy](https://web.archive.org/web/20201215182132/https://support.apple.com/en-us/HT211965))

That's fine though, because technically, the ProRaw file is just the latest version of a DNG (Digital Camera Negative) file, with an [open specification here](https://helpx.adobe.com/content/dam/help/en/photoshop/pdf/dng_spec_1_6_0_0.pdf) from Adobe. DNG already has an [FDD here](https://www.loc.gov/preservation/digital/formats/fdd/fdd000188.shtml), but an earlier version. It's also "not raw" (again, the above Lux blog post goes into a lot more detail here), essentially prepped in a way that it's already done the optional "de-mosaic" process, part of what would make the file "raw" to begin with. So there could be an argument made between DNG 1.6 and ProRaw being the same format, and an argument for ProRaw being different from DNG 1.6 because it always has some attributes and have already been processed in specific ways. Where's the line, with a format? What do you think?