---
layout: post
title: "Artist_Exhibition-copy (FINAL)(2).mov: Preserving diacritics in filenames as significant properties in media conservation"
date: 2019-06-17 09:00:00 -0500
---

![welcome](/images/welcome-sign.gif)

Hi! This is a blog post. I am gonna talk about this in a way that assumes no
character encoding knowledge. Alternatively, if this isn't new news to you, I am
sure you have plenty of things to add but this is a blog post, not a Masters
thesis, so stay mellow! I am trying to keep this concise, but it's hard.

This blog post is, however, written within the context of libraries, archives,
and museums doing digital preservation work, so there may be some assumed
knowledge within. A lot of field-based context can be summarized in Elvia
Arroyo-Ramírez's excellent writing/presentation entitled [Invisible Defaults and
Perceived Limitations: Processing the Juan Gelman
Files](https://medium.com/on-archivy/invisible-defaults-and-perceived-limitations-processing-the-juan-gelman-files-4187fdd36759),
discussing the details of digital archival processing and the racial and
Western-centric implications of considering certain characters to be "illegal."
This is really essential reading for the field of digital preservation, so I
recommend it over this one, for sure.

For some quick context, some institutions rename their files, and some consider
the original filenames as something significant to the artwork and therefore
something that must be retained throughout systems. As a person who works on
open [software](https://www.archivematica.org/en/) that must suit all different
kinds of use cases, it is not up to me to come down on either side and cast
judgment; it is my duty to make sure the software works for as many places as
possible, and giving people the freedom to come up with workflows that work for
them and their institutional needs.

To be up-front right away: character encodings are a whole big mess of a world,
and there are [a ton of
them](https://en.wikipedia.org/wiki/Character_encoding#Common_character_encodings).
A simple analogy is that it's not unlike when there are new emoji released but
you haven't updated your phone, so all you see are these little blank boxes. I
like that they are pejoratively called "tofu". When a machine is running into
one of these totally innocuous-looking accented characters, it looks like
"character encoding" but it is actually more like "character enc💣ding". And the
bomb emoji is accurate because it just blows up even though everything is looking
fine!

![sign up today](/images/sign-up-today.gif)

When looking in a browser viewer, the two files with the same name but different
character encodings might look the same, because web browsers force UTF-8
encoding onto all the text being read on the page. Operating systems may make
this decision as well.

But when looking at files using the command line on the hosted server, the
original files written with a different character encoding (let's say
`my-éxample.mkv`) look like this:

`my-�xample.mkv`

The above could be referred to as
[mojibake](https://en.wikipedia.org/wiki/Mojibake), which is a subset of this
same subject that has a very long and detailed wikipedia page that gives many
examples of character encoding misalignment and things going awry.

To talk through what happens when a computer comes across `my-�xample.mkv`, we
have to go way back into [How Computers Work
101](https://training.ashleyblewer.com/presentations/computers#1) and think
about bits and bytes. (⚠ Incoming oversimplification alert ⚠) Computers read
everything as a sort of stream of data, and character encodings help to
understand how to handle that data. When it sees a string like above, it starts
moving down the list.

- `m` is `01101101` in binary! next
- `y` is `01111001` in binary! next
- `-` is `00101101` in binary! next
- `é` is `11000011 10101001` AHHHHHH 😱 WHY IS THIS SO BIG???

If the computer has been chomping on letters expecting to take up a certain
amount of space, because its been told that every letter can only take up a byte
of space, and it suddenly comes across some two-byte scenario, it just
explodes. There are a lot of other reasons why characters may cause an explosion
and this is just one of them.

Unlike [something like
apostrophes](https://www.wsj.com/video/how-genius-used-morse-code-to-track-its-lyrics/88EA4852-4543-4D50-A313-A613FBD00EC0.html),
the characters look identical to us humans but are different deep in the
bitstream, which matters a lot to computers. To again
use emoji as an example, some symbols are just made to look a certain way, and
others use something called [zero-width join
operators](https://en.wikipedia.org/wiki/Zero-width_joiner) to "smush together"
a letter and an accent, and this is how emoji are able to [apply skin tones to
people emoji](https://emojipedia.org/zero-width-joiner/).

There's a lot more to say about character encoding, but that's the basics, to go
from the first point (that this is really complicated) to the next point: because
it's a hard problem, there is no one perfect tool to magically deal with all
of this. But first, a detour into how I get into these mystery file encoding
situations.

![drivers-tournament](/images/driv.gif)

[Archivematica](https://www.archivematica.org/en/) can accept diacritics in
general (well, especially in version 1.8+, things have been a bit dicey in the
past), but there are so many encodings out there and no one good tool to convert
them all to UTF-8, which is what we want to use. Like I said at the front,
Archivematica is not made for one use case, but potentially every possible use
case. This is apparent in other parts of the preservation process such as
normalization (some would never, some would, and others disagree on file
formats) or validation ([JHOVE](https://github.com/openpreserve/jhove)
identifies files as well formed, valid, both, or
neither, and bytestream handling is nuanced based on institutional requirements
and file formats, but Archivematica displays a binary yes/no in terms of
passing/failing). So sometimes the best answer is the one that works most of the
time for the most amount of people.

Because of my job, I come across files after acquisition and curation, after
temporary storage, sometimes after extraction, and at the point of moving them
into long-term preservation storage. I am familiar with the environments I am
working in, and Archivematica runs in a (typically virtualized) Linux
environment (although that can be Ubuntu or CentOS or RedHat [which isn't
*supposed* to be different but.. computers]). I usually don't have context into
the file's lifecycle prior to that, like the operating system of origin (or
initial transfer into digital from an analog carrier), the system used for any
kind of arrangement of materials, the system used to extract contents (in the
case of disk imaging), or the system used for temporary, mounted storage. 

When I come across a problem with a file, it's because someone with a support
contract with Artefactual is having a problem, and all they know is "this isn't
working." First, I have to sort out whether the origin of the issue comes from
the Archivematica application itself (Python/Django) or one of the dozen-or-so
piece of software used by Archivematica (BagIt, ExifTool, MediaInfo, JHOVE,
FITS, just to name a few). Is this a problem with
the software dependency (not in my control, but potentially in my control to
fix) or Python/Django (in my control, but software has release cycles, so not
necessarily something that can be immediately resolved)? This is assuming it is
not the third option (and it frequently is this option): there is an issue not
with any of the software, but the server space is not adequately commissioned
(not enough space on device, competiting systems on a shared server, CPU or RAM
issues). But I am going to leave that last potential batch of issues out of
this.

The point is, there are a lot of things about the origin of a file that I don't
necessarily know. Sometimes I can find out that information (if the archives
team in question has a good relationship with their IT department, or they were
also the processors of the filesets they are wanting to process within
Archivematica) and sometimes I can't. Sometimes I have other context clues, like
a folder being named "G4 Laptop", to narrow down what might cause these files to
have a particular kind of file encoding, or I might be able to guess the
language of origin based on words in the filename, and then sort out what
encoding was used on this filename.

![chosen to serve](/images/chosen-to-serve.gif)

## Know the encoding

If I know the encoding, I can try using the `convmv` tool to convert from one encoding
to UTF-8. The command is like this:

`convmv -f SOURCE_ENCODING -t UTF-8 path/to/file.ext -o path/to/new-file.ext`

If you are on a computer with this installed, you can pull up the list of
encodings supported by running `convmv --list`. If not,
[here](https://gist.github.com/ablwr/098ec913c812b36b1e36aa4b52d8e338) is a
gist. It is a lot! But to do conversion using a tool like this, you have to
know what you are converting from, before you can convert to something else.
`convmv` can't guess what encoding is which. A potential solution is to convert
everything to ASCII and then to UTF-8, but that would defeat the point of trying
to preserve the parts of the filename that are significant, and would blow away
any diacritics or significant symbols and still potentially leave a bit of a
mess.

`convmv` also isn't going to change the contents of a file, and for that you'll
have to use `iconv`. You may need to use both. This can be applied to everything
in a fileset. I list out other potential tools at the bottom of this post, but
none of them can definitively guess and correct encodings.

## No idea about the encoding

If I know what the character is supposed to be but don't know the original
encoding, I can manually rename the file. This is a good solution if you have a
dozen or so files, but this is not scalable if you are working with entire
extracted filesystems with potentially hundreds of files.

`mv my-�xample.mkv my-éxample.mkv  # . o O (now I'm in UTF-8)`

## I know my systems and the files are still messed up

Another thing I alluded to earlier is that the files could be set into a
disarray in transit -- so the original encoding was passed through a carrier and
then into the system I am now working with, and throwing things off. This can
also cause confusion with things like [carriage return
lines](https://en.wikipedia.org/wiki/Carriage_return). A couple of years ago I
was trading a CSV back to someone for a project we were working on, and he kept
complaining that I was adding a bunch of junk in the CSV, at the end, even
though we were both using Macs at the time. We eventually realized that because
the CSV was passing through email servers, and those servers were opening and
checking on our CSV, and the servers must have been DOS-based at some point, it
was adding all of these carriage returns to our "pure" Mac-based workflow's
files.

The issue could also be with a configuration setting between a mounted hard
drive and the processing space you are working on, and without a configuration
set in a specific way, it could be passing the character encoding over without
handling or converting to UTF-8, or it attempts to convert to UTF-8 by guessing
the character encoding and getting it wrong, mangling the files in the process.

![chinese firefighters](/images/chinese.gif)

## Guess the encoding

Sometimes I make a guess of what the encoding is, I use the `file`
command, like this:

`file -i path/to/file.ext`

The `file -i` command will sometimes give you the encoding, or sometimes it will
give you back the code page used for encoding a document. Introducing [code
pages](https://en.wikipedia.org/wiki/Code_page). This can help when tracking
down the original encoding in a way different from the above and can help with
debugging the issue below.

This might work for you if you are processing a collection and have a lot of
time. I don't have a lot of time, because I have so many other things to work
on and people to work with, and overall I run into this problem because its
preventing someone from doing one specific thing -- processing files within
Archivematica -- and thusly my goals are different.

## The encoding already is UTF-8

An issue I have run into is that while a folder that is called
something like "rue Séguier" will return UTF-8 as a character encoding, it
doesn't mean that everything is still fine. UTF-8 is a standard, but just
because it is a standard doesn't mean it has always been stable, and it doesn't
mean that systems agree with each other about how to interpret that standard. If
you are dealing with files from Mac operating systems from the 1990s and early
2000s, the interpretation for encoding may be different, even if using the same
rules. So, sometimes files being in UTF-8 isn't enough to resolve the problem.

In Archivematica, there is a step to clean up filenames, and this step stores
the original filename in the METS metadata (sort of the single-source-of-truth
for representation of many assets) and replaces non-ASCII characters (a more
technically accurate and less insensitive way of describe files, better than
"illegal") with underscores.

The great thing about open source software is people have the power to change
the software for the better, usually by funding the development of a feature
that, for example, would make this service optional or would better handle
diacritics and conversion into UTF-8. The not-so-great thing about open source
software is funding flows like a trickle and feature requests flow like a
waterfall, and no one has stepped up to fund something like this. Elvia's
aforementioned
[post](https://medium.com/on-archivy/invisible-defaults-and-perceived-limitations-processing-the-juan-gelman-files-4187fdd36759)
has been very influential and has brought attention to this topic, but no
organization has yet to take action, beyond Artefactual as a company taking on
the unpaid maintenance work to patch as much as possible.

![one tru bytch](/images/one-true-bytch.gif)

So, back to the stewards of video art, of extracted disk images and early
computer art, of old laptops belonging to famous artists, et al and ad
infinitum. I suppose in an ideal situation, we are taking care to retain and
care for these aspects of filenames: It is significant that the artist was
editing video on a Portuguese-language Mac, it matters that this author was writing
her last unfinished novel on the latest-at-the-time laptop with an inconsistent
encoding pattern, or this network-based art installation is presented in English
but the operating system prefers Cyrillic. But practically speaking, is
retaining the language but converting it to an interoperable encoding standard
appropriate, when the difference is indistinguishable to human perception?
Should it be tossed in the trash like a .DS_Store? For
those of you who work in media conservation, where do you draw the line with
"significant properties"? What is meaningful, when and where is it meaningful,
and how is it meaningful? Does this fit into the artist's intent, or
contextualization of an artwork, historical significance and research, or
significant in the accurate presentation and replication?

## Conclusion?

We are increasingly approaching a UTF-8-standardized world, so this will pop up
less and less in daily practice (and we've already made a lot of advancements),
but just like writing in cursive, the familiarity will become less familiar,
and it may get harder for average folks to know how to deal with these
unreadable symbols in the future, when looking into the past.

Speaking of the advancements that have been made towards standardizing text
across systems, I recommend this talk: [!!Con West 2019 - Misty de Méo: Let’s
translate old video games! How do they even
work?!](https://www.youtube.com/watch?v=t37Cr3FDyvU) and to take a look at how
the [URL for Misty's speaker bio page on the !!Con West
website](http://bangbangcon.com/west/speakers/#misty-de-m-eacute-o) turned her
accented é into "-eacute-", which is the HTML escape character entity for é!
[Here's a table](https://www.w3.org/MarkUp/html3/latin1.html) as a reference.

Also at !!Con (East, 2018), Ahmed Abdalla gave a talk on [creating an Arabic
Programming Language](https://www.youtube.com/watch?v=eCxqAr7LjW8), taking a lot
of these concepts into consideration.

![world bar](/images/barworldflags.gif)

All of this manifests itself in more than just files coming off of legacy
file systems, and even affects major systems like phones, cars, and email
software, resulting in lost messages, mixed messages, or an inability to play
messages. For example:

- [Emojipedia: Why Am I Seeing Question Mark
   Boxes?](https://blog.emojipedia.org/why-ios-is-spreading-question-mark-boxes/)
- [Reply All: #140 The Roman Mars Mazda Virus](https://gimletmedia.com/shows/reply-all/brh8jm/140-the-roman-mars-mazda-virus)
- [English StackExchange: What does a single letter “J” mean in emailing?](https://english.stackexchange.com/questions/46829/what-does-a-single-letter-j-mean-in-emailing)

Here's a short list of some command-line tools that are available (including
ones I mentioned and ones I didn't):

- `chardet3` or `chardetect3`
- `file`: Get basic information about files
- `fndec`: Guesses encodings of file names, written in Go by Ross Spencer. [Link
  to Github repo](https://github.com/exponential-decay/fndec)
- `iconv`: You want to change the text within a document, not the filename
- `dos2unix`: If you know you are coming from a Windows platform to a Unix one
- `enca` and `enconv`: If you are working with Eastern European encodings
- `encguess`: If you are on Debian
- `uchardet`: If you want yet another option (I didn't really test this, the man
  page is very sparse)
- `chardet`: You want to use Python ([Link to Github repo](https://github.com/chardet/chardet))
- `uconv`: converts using Unicode as a "pivot encoding"

Unless otherwise noted, you can get them from Linux package distros.

Some other significant resources:

- [Joel on Software: The Absolute Minimum Every Software Developer Absolutely,
  Positively Must Know About Unicode and Character Sets (No
  Excuses!)](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/)
  (this is from 2003 but still relevant and cited everywhere)
- [The beets blog: our solution for the hell that is filename encoding, such as it is](http://beets.io/blog/paths.html)
- [Falsehoods Programmers Believe About Names](https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/)
- ICYMI at the top, Elvia Arroyo-Ramírez's [Invisible Defaults and Perceived
  Limitations: Processing the Juan Gelman
  Files](https://medium.com/on-archivy/invisible-defaults-and-perceived-limitations-processing-the-juan-gelman-files-4187fdd36759)
- [The beets blog: our solution for the hell that is filename encoding, such as
  it is](http://beets.io/blog/paths.html)

Thanks to the institutions I've worked with over the past year who have had
these problems for your patience. You know who you are!

Happy encoding, transcoding, and decoding!

![author with cat](/images/cat-rhizome-shirt.jpg)

