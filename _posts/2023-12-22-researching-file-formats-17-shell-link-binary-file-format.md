---
layout: post
title: "Researching file formats 17: Shell link binary file format"
date: 2023-12-22 08:00:00 -0500
tags: [file formats, fdds]
---
This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [Microsoft Windows Shortcut File
](https://www.loc.gov/preservation/digital/formats/fdd/fdd000596.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

Shell Link Binary File Format  
Formal name: Shell Link Binary File Format  
Informal name / also known as / previously known as: Microsoft Windows Shortcut  

Link files are a little bit sneaky. They appear on the Windows graphical user interface (the Desktop, folders, et al) without a file extension and with an illustration of an arrow in the bottom left corner, but no visible file extension -- Windows hides that. Also any folder that is "My Recent Documents" or whatever will be composed of these link files, too.

For a long while, this file was opaque and had to be reverse engineered for any analysis. Microsoft has since fully put the specification and history [online](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-shllink/16cb4ca1-9339-4d0c-a68d-bf1d6cc0f943), at least since 2010. (But the file has been around for a good many years before that... like 15 years.) Prior versions are acknowledged in the version history on the website and in the specification draft but not available.

This format let me explore the malware potential of files for a little bit, as LNK files have been used to make computers go boom-boom-boom, like this [malware case](https://www.theregister.com/2023/01/23/threat_groups_malicious_lnk/). I can really appreciate the infosec community when they do so much open reporting on vulnerabilities, and in general the formal practice of private disclosure and, if necessary or at the appropriate time, public disclosure.

I like how malware always have cute names. One of the ones impacting this format is called ["Raspberry Robin"](https://redcanary.com/blog/raspberry-robin/). It's a worm!

