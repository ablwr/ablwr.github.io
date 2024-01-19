---
layout: post
title: "Researching file formats 21: bzip"
date: 2024-01-19 09:00:00 -0500
tags: [file formats, fdds]
---

Last week was gzip, this week is bzip. Or, I think, bzip2. I struggled with what to say about gzip, but bzip/bzip2 is more interesting because of PATENT PROBLEMS! 

bzip2 is based off of its predecessor bzip. bzip2 is widely more popular, bzip isn't really used so much anymore, because of some patent problems. There was this dude running around in the 90s being a jerk and suing everyone he could for a basic algorithm, so people had to just make better algorithms, which wasn't even very hard, but it did cause a lot of headaches. I'm oversimplifying. I found [this website](https://ethw.org/History_of_Lossless_Data_Compression_Algorithms#Legal_Issues) to be useful in explaining things better, and in general explaining a lot about the history of compression formats -- recommended! 

bzip2 was a rewritten version of bzip, primarily done to avoid any potential patent issues with the original bzip. Both were written by Julian Seward. Essentially, bzip was created, there were potential patent issues, and the author removed the original software and replaced it with bzip2. So bzip2 is the way to go.

I like this note about y2k issues [from the bzip2 homepage](https://web.archive.org/web/20050207055319/http://www.bzip.org/): "I am not prepared to offer you any assurance whatsoever regarding Y2K issues in my software." 

What else? bzip2's header, when converted from Hexadecimal to ASCII, is "BZh." (Wikipedia cites the magic number as BZh instead of in hex; hex is cited in most other places.) BZ for BZip, and the "h" is for "Huffman coding," the compression algorithm used with bzip2. bzip files will have '0' instead of 'h' as the third byte in the header (and '0' maps to '30' in hex, compared with 'h' which maps to '68').