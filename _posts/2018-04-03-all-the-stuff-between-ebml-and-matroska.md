---
layout: post
title: "All the stuff between EBML and Matroska"
date: 2018-04-03
---

![magic hat](/images/magic-hat3.jpg) 

*Update with more information below!*  

I was opening up a small Matroska file in my hex editor (I use Hex Fiend, I don't know if it's the best, but it works well for me) and I identified the Matroska magic numbers and the EBML magic numbers, but there was some ... other stuff interrupting them.

The file starts with the EBML magic numbers `1A 45 DF A3` and then something happens here `01 00 00 00 00 00 00 23 42 86 81 01 42 F7 81 01 42 F2 81 04 42 F3 81 08 42 82 88` and then Matroska's magic: `6D 61 74 72 6F 73 6B 61`

What is all this in between EBML and Matroska magic numbers?

[To the specification!](https://github.com/Matroska-Org/ebml-specification/blob/master/specification.markdown#ebml-header)

- `01 00 00 00 00 00 00 23` I assume just extra blank space with a bonus 23, maybe saved empty space.  
- `42 86` is the hex for EBMLVersion Element followed by `81 01`  
- `42 F7` is the hex for EBMLReadVersion Element followed by `81 01`  
- `42 F2` is the hex for EBMLMaxIDLength Element followed by `81 04`  
- `42 F3` (see a pattern?) is the hex for EBMLMaxSizeLength Element followed by `81 08`  
- `42 82` is the hext for DocType Element followed by `88`  

I'm not sure if the `81` is just there as a spacer, but the last number in these blocks do have the expected output according to the EBML spec. 1, 1, 4, and 8. DocType Element doesn't necessarily fall into line here, but maybe `88` is, like, a super big spacer or in some way indicates the size of the data that is about to come? No, actually I just don't know but I feel okay about that.

I also used [this chart](http://www.aboutmyip.com/AboutMyXApp/AsciiChart.jsp) to see if there was any meaning in binary, that is the B in EBML after all, but no dice. And [this converter and it's siblings](https://www.rapidtables.com/convert/number/hex-to-binary.html) were helpful too.

I've been working with the EBML and Matroska specs and their standardization for a long time, so I guess I already "knew" all of this, but I didn't really-really "KNOW" it until I did some hex-reading directly on my own. I really had to step through -- and the `23` threw me off, but as soon as I saw the meaning behind `0x4286` it all made total sense, like that "duh, of course!" moment of it being other significant properties at the head of an EBML file before the Matroska file could begin, since Matroska files are derived from EBML files. I'm confident that the hex after the Matroska magic numbers follow the same rules and are outlined in the spec, but my curiosity has been satisifed for now.

**Update!**  

This update comes from [Dave Rice](http://dericed.com) and tidied up into a paragraph by me:  

The block `01 00 00 00 00 00 00 23` is just an inefficiently represented element size saying that the data of the element is 23 bytes, the 0x01 or 0x00000001 at the beginning means that the length of the size is 8 bytes (tally of the leading binary 7 zeros plus 1). It could more efficiently be written as 0xA3, or 0b10100011, (zero leading binary zeros plus 1, is one so this size expression is only 1 byte long). If you omit the leading data of both expressions up to the first 0b1, then the remaining value stored is the same, 0x23 aka 35. Likewise, 0x81 is common in EBML as it means that the element size is one byte (0x81 = 0b10000001), so it's a one byte long expression that stores a value of 1. These values are all Variable Integers, a way to store a flexible length size. It helps avoid the situation where you have size limits like in WAV.

But basically with the Element IDs and sizes the count of leading zeros plus one tells you the length of the id/size, then there’s a single 1 bit as a marker, and then the remaining bits are the value of the element. So 0x88 (or 0b10001000) is a statement of size that the element data is eight bytes long.



