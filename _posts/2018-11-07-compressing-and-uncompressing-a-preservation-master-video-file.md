---
layout: post
title: "Compressing and uncompressing a preservation master video file"
date: 2018-11-07 21:50:00 -0500
---
The other day, a friend of mine asked me...

"so let's say to save space i want to take all my 10-Bit Uncompressed masters and encode them as FFV1 to save space  
but then, for whatever reason, i want to get them back as 10-Bit files  
can i just like, run them back through ffmpeg and tell it to make uncompressed files?"

And I am here to tell you all: Yes, you can! And here is how you do that, so you can test it out for yourself.

For some context to people hitting this site without an audiovisual preservation background, a standard recommended preservation format is an uncompressed video stream with 4:2:2 chroma subsampling, and with each sample representing 10 bits of data. [This Library of Congress website](https://www.loc.gov/preservation/digital/formats/fdd/fdd000353.shtml) speaks more in-depth about this. This is a large spectrum of information, and it takes up a lot of space. Another recommended preservation format is FFV1, an open, losslessly compressed codec made by FFmpeg and is currently being standardized through the Internet Engineering Task Force ([here](https://datatracker.ietf.org/wg/cellar/about/)). You can learn more about all this stuff [here](https://training.ashleyblewer.com/).

To follow along, you'll need to have `ffmpeg`, `mediainfo`, and `md5deep` installed on your computer. (You could also use `hashdeep -c md5` instead of md5deep.)

* ffmpeg: [http://ffmpeg.org/](http://ffmpeg.org/)
* mediainfo: [https://mediaarea.net/en/MediaInfo](https://mediaarea.net/en/MediaInfo)
* md5deep: [http://md5deep.sourceforge.net/](http://md5deep.sourceforge.net/)

OK, now we are ready to test this out ourselves. First, we need a file. Fortunately, `ffmpeg` can make one for us, which is cool.

`ffmpeg -f lavfi -i mandelbrot=size=640x480:rate=25 -c:v v210 -t 5 uncompressed.mov`

Great! Do we have what we want? Let's use `mediainfo` to see:

`mediainfo uncompressed.mov`

The results should show that this is a YUV v210 mov file, just like we ordered.

Now we need to turn this into an FFV1 file. Here's how we do that, taken from [ffmprovisr](https://amiaopensource.github.io/ffmprovisr/#create_FFV1_mkv). As a bonus, we get a text file with the md5 checksums for each frame. This is another perk for using FFV1! I also took the liberty of changing wrappers, and making it an .mkv.

`ffmpeg -i uncompressed.mov -map 0 -dn -c:v ffv1 -level 3 -g 1 -slicecrc 1 -slices 16 -c:a copy ffv1.mkv -f framemd5 -an framemd5.txt`

Now we have two files, an uncompressed 10bit mov file, and an ffv1 encoded video in a Matroska file, great for preservation storage. Now, let's take that Matroska file and turn it back into an uncompressed 10bit file.

`ffmpeg -i ffv1.mkv -c:v v210 uncompressed-again.mov`

OK, now we have two uncompressed .mov files. Let's check up on these files by generated an md5 checksum for each of them. 

`md5deep uncompressed.mov`  
and  
`md5deep uncompressed-again.mov`  

Your results should be this. Your checksum should even match.
`19b70aad2af65586ba54638f3d45ffd3  /home/ashley/Testing/uncompressed.mov`  
and  
`19b70aad2af65586ba54638f3d45ffd3  /home/ashley/Testing/uncompressed-again.mov`  

This works if the first and final files are .mov. If the first file is an MOV and the final is uncompressed wrapped in an MKV, the checksum won't be the same because they are using a different wrapper. But if you start with an MKV and end with an MKV, they won't also match because of how Matroska wrappers are structured. If you run a checksum on only the video stream of both of the files, that will match, it just takes a little more work to see the difference. But that's a different blog post for another time...
