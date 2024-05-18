---
layout: post
title: "Researching file formats 31: XYZ Point Cloud"
date: 2024-03-29 07:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [XYZ Point Cloud](https://www.loc.gov/preservation/digital/formats/fdd/fdd000617.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

After a handful of difficult and technically (or socially/politically) complex formats, it was nice to work on this simple (if unspecified) format, taking me back to one of the earliest formats I worked on, [FASTA](https://bits.ashleyblewer.com/blog/2023/08/11/researching-file-formats-1-fasta-database-format/). This format originally belonged in that initial category (see [RGBE Image Format](https://bits.ashleyblewer.com/blog/2023/09/08/researching-file-formats-5-radiance-rgbe-image-format/)), but there was a mix-up. While it is structurally similar to FASTA, it is a 3D format and has the same [quality and functionality factors](https://www.loc.gov/preservation/digital/formats/fdd/fdd_explanation.shtml#factors) as the rest of this set.

This format simply stores point clouds (a way to articulate geographic shapes) aligned with the [Cartesian coordinate system](https://en.wikipedia.org/wiki/Cartesian_coordinate_system), which is, as the format name implies, X, Y, Z.

The format starts with a comment (represented by a # and the text), and then coordinates separated by spaces, with new lines for each next point. That's it! That's the format.

There's also some variations that include adding color, so those follow the syntax of `X Y Z R G B`!

At the same time, while this format was simple, it also poses a challenge of not being officially documented in many places, as noted in this [stackoverflow post](https://stackoverflow.com/questions/41267210/point-cloud-xyz-format-specification) stating that there are no official docs. Anyway, more to come on that when the official FDD is published.

Disambiguation: This format was set to cover the one I'm describing above, but there's another format that is a text-based simple data format also called XYZ, used for [storing chemicals](https://en.wikipedia.org/wiki/XYZ_file_format). That one is described [here](https://www.cgl.ucsf.edu/chimera/docs/UsersGuide/xyz.html).