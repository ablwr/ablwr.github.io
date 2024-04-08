---
layout: post
title: "Researching file formats 13: vCard (virtual business cards)"
date: 2023-11-24 07:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [Virtual Card Format (vCard)](https://www.loc.gov/preservation/digital/formats/fdd/fdd000616.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

vCard or VCF: Virtual Card Format? Virtual Contact File? vCard File? Sources are not consistent with this.

This format has a lot of official specifications and extensions, lots of updated versions during the standardization process, several major versions, and a few different owning organizations. 

See:
- [RFC 2425](http://tools.ietf.org/html/rfc2425) - A MIME Content-Type for Directory Information
- [RFC 2426](http://tools.ietf.org/html/rfc2426) - vCard MIME Directory Profile
- [RFC 2739](http://tools.ietf.org/html/rfc2739) - Calendar Attributes for vCard and LDAP
- [RFC 4770](http://tools.ietf.org/html/rfc4770) - vCard Extensions for Instant Messaging
- [RFC 6351](http://tools.ietf.org/html/rfc6351) - xCard: vCard XML Representation  
- [RFC 6473](http://tools.ietf.org/html/rfc6473) - vCard KIND:application
* [RFC 6474](http://tools.ietf.org/html/rfc6474) - vCard Format Extensions: Place of Birth, Place and Date of Death

That's nice but it's also a lot to get through!

Resources keep using the acronym MUA, which I immediately translate to "Makeup Artist" but in this context, it's "Mail User Agent." 

This format, and a few others in this "email" section, had me digging into very old scanned copies of books that have started to become digitally crunchy.

Please enjoy this difficult-to-read text that describes what an image file looks like as text:
![difficult-to-read text describing what an image looks like in text](/images/vcf-text.jpg)

The biggest drama working with this format is seemingly people coming up with what the .vcf extension stood for without any real reasoning, so some places say it stands for Virtual Card Format (including the outline of the description from Library of Congress), some say Virtual Contact File (including Wikipedia), and some say vCard File. Google also said "virgin card" because it was conflating urban dictionary knowledge with file format knowledge, but it's not that one, probably.

This example is pretty trivial, since it's just the name, but sometimes things aren't so trivial, and people just pass around lore without really knowing where it comes from. Something I appreciate about this format is everything must be cited, so you can't just make a few connections in your head (which I very much want to do all the time), you have to really prove that its right, and from valid sources. I think valid sources gets a liiiiittle loosey-goosey when it comes to some more modern file formats, because there is a lot of good advice that comes out of things like forums, even if it's just Some Person Online Saying Something. Sometimes that knowledge can be tracked back to something more valid, or at least point me in the right direction. Other times, I'm like well... I think this is as close as we are gonna get. 

