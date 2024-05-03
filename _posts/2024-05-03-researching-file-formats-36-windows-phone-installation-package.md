---
layout: post
title: "Researching file formats 36: Windows Phone Installation Package"
date: 2024-05-03 07:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [Silverlight Application Package](https://www.loc.gov/preservation/digital/formats/fdd/fdd000595.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

Okay, this was a fun one! If you remember using Netflix in the early-to-mid 2010s, you might remember having to download this extra thing called Silverlight in order to stream video. For reasons that I would love to have a full-length book on, that same package application, Silverlight, is also the same as the short-lived Windows Phone installation package, or XAP ([pronounced "zap"](https://learn.microsoft.com/en-us/archive/blogs/katriend/silverlight-2-structure-of-the-new-xap-file-silverlight-packaged-application)).

In addition to the confusion around the two use cases (phones and Silverlight), XAP is also the extension for XACT Audio Projects, which is also now called Microsoft XNA Game Studio.

Both Windows Phones and Silverlight are discontinued products.
- Windows phones ran from [October 21, 2010 to June 2, 2015](https://en.wikipedia.org/wiki/Windows_Phone)
- Silverlight existed from [September 5, 2007 to January 15, 2019](https://en.wikipedia.org/wiki/Microsoft_Silverlight)

Like the two previous package formats, XAP files are also essentially just ZIP files structured in a specific way. These have two manifest files and some DLLs (containing the compiled version of the application).

Documentation is sparse, all around.

XAP format was replaced by APPX format, although not for long since Windows Phones had a less-than-5-year lifespan.