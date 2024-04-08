---
layout: post
title: "Researching file formats 1: FASTA database format"
date: 2023-08-11 07:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [FASTA Database Format](https://www.loc.gov/preservation/digital/formats/fdd/fdd000622.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

First format: FASTA!

This is a format used to store nucleotide acid or amino acid data.

You can see [examples of what this looks like here](https://www.ebi.ac.uk/seqdb/confluence/display/JDSAT/Multiple+Sequence+Alignment+Tool+Input+Examples).

To me, this format looks a bit like screaming into a void. I don't know if people call it "FASTA pasta" but that feels like an applicable way to think about it.

If you download just a lil bit of the [human genome](https://hgdownload.soe.ucsc.edu/downloads.html) (Look for the latest "[Sequence data by chromosome](https://hgdownload.soe.ucsc.edu/goldenPath/hg38/chromosomes/)") and unwrap it (it's gzipped), you'll get something that [sounds](https://en.wikipedia.org/wiki/Bouba/kiki_effect) a bit impatient at first:

```
➜ head chr1.fa
>chr1
taaccctaaccctaaccctaaccctaaccctaaccctaaccctaacccta
accctaaccctaaccctaaccctaaccctaaccctaaccctaaccctaac
cctaacccaaccctaaccctaaccctaaccctaaccctaaccctaacccc
taaccctaaccctaaccctaaccctaacctaaccctaaccctaaccctaa
ccctaaccctaaccctaaccctaaccctaacccctaaccctaaccctaaa
ccctaaaccctaaccctaaccctaaccctaaccctaaccccaaccccaac
cccaaccccaaccccaaccccaaccctaacccctaaccctaaccctaacc
ctaccctaaccctaaccctaaccctaaccctaaccctaacccctaacccc
taaccctaaccctaaccctaaccctaaccctaaccctaacccctaaccct
```

and if you look a few lines, more, it starts to sound more agitated:

```
CACCCTGCCAGGGAGCCTCCCGTGGCACCGTGGGGACACAAAGGAACCAG
GGCAAAGCTCCCTCAGCCCCATTCAAAGAGGCCTGGCCCACAGGCTCACG
GAAAGTCAGCCTCTCATGCCCCGAGAGCTGAGTGCAAGGGAGAGGCAGCG
CTGTCTGTGCTTCCCATGCAGAAGCACCCCCCTCCCACCCCTGTGCAGGC
CGGCCTTCGCGGCAGACCACCATACACCACGTTCCAAGCCACACTGAGGC
CTCCCTCCAAGCCTGCAGCCCCCATTTCCAGACCCTGCCAGGGCAACCTG
CATATCCACCTCCCTACCCTGCCCCCCTCTTCCAGGAGTCTGCCCTATGT
GGAGTAAGCACgtggttttcctcttcagcaactatttcctttttactcaa
gcaatggccccatttcccttggggaatccatctctctcgcaggcttagtc
ccagagcttcaggtggggctgcccacagagctcctcagtctaagccaagt
ggtgtgtcatagtcccctggccccattaatggattctgggatagacatga
ggaccaagccaggTGGGATGAGTGAGTGTGGCTTCTGGAGGAAGTGGGGA
CACAGGACAGCATTCTTTCCTGCTGGACCTGACCCTGTGTCATGTCACCT
TGCTACCACGAGAGCATGGCCTGTCTGGGAATGCAGCCAGACCCAAAGAA
GCAAACTGACATGGAAGGAAAGCAAAACCAGGCCCTGAGGACATCATTTT
AGCCCTTACTCCGAAGGCTGCTCTACTGATTGGTTAATTTTTGCTTAGCT
TGGTCTGGGGAGTTCTGACAGGCGTGCCACCAATTCTTACCGATTTCTCT
CCACTCTAGACCCTGAGAAGCCCACGCGGTTCATGCTAGCAATTAACAAT
CAATCTCGCCCTATGTGTTCCCATTCCAGCCTCTAGGACACAGTGGCAGC
CACATAATTGGTATCTCTTAAGGTCCAGCACGAGGTGGAGCACATGGTGG
```

And if you get to the bottom, it sounds like it just wore itself out and is ready to fall asleep:

```
➜ tail -15 chr1.fa 
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNN
```

Anyway, that's FASTA. It's considered a database format? But it's a pretty simple database. It's a text file that can contain multiple segments, with a ">" to start the segment and give one line for a comment, and then the next part of a segment is the data sequence. It can be big enough to be a database, and can be imported into analysis systems (like [BLAST](https://blast.ncbi.nlm.nih.gov/doc/blast-topics/) from the National Center for Biotechnology Information), but it's not a database in the way that we typically think of them these days (an entire relational management system that uses a query language to retrieve parts of the whole).

It's cute to read a paper from 1985 with phrases like:
"For example, comparison of a 200-amino-acid sequence to the 500,000 residues in the National Biomedical Research Foundation library would take less than 2 minutes on a minicomputer, and less than 10 minutes on a microcomputer (IBM PC)."  
and   
"In the original algorithm, identities or groups of identities are rapidly located with a tool known in computer science as a lookup table (8)."

What else is fun about this format?

Someone on Mastodon (link is now dead, so I removed it) asked about the difference between uppercase and lowercase, which got me thinking about how standards may start out strict (only use uppercase; lowercase values will be mapped to uppercase), but through time and the need for more ambiguity, they can start holding meaning beyond the scope of the specification/standard (to indicate repeating patterns OR to indicate assumptions, maybe other things). This format doesn't really have a true specification, so there's a lot of "folksy" nuance, except that the folksiness is being determined largely by the U.S. National Center for Biotechnology Information. So what they say is what goes, and becomes this stronger standard but still an informal one, "recommended guidelines" rather than requirements. They do [document their expectations](https://www.ncbi.nlm.nih.gov/genbank/fastaformat/) as it differs from the original proposed format, mostly around coming up with an ID for each segment, or [expectations around the data structure](https://blast.ncbi.nlm.nih.gov/doc/blast-topics/) for ingest into their search tool, BLAST, but it doesn't account for, say, the nuances of using upper and lowercase to declare whether the sequence is definitely or probably the right thing. 

There's a lot to think about there, around how a format is used in practice versus how it was initially proposed, and how that general-use practice takes over but is never really clearly documented, and so there's this big gap between the rules and what people actually do. It also makes it challenging to write in a formal, assertive manner. :) 

Anyway, I initially thought that lowercase was used for ambiguity of a format, but rather it means something more like "assumed data repeats in this pattern here" so it can be easily skimmed over, or interpreted in a specific way using software (like greying it out). 

Those are the informal notes for this first format! Next up (next week): MySQL Table Definitions.
