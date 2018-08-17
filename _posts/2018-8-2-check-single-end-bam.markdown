---
title: "Checking whether reads in BAM are paired-end"
layout: post
date: 2018-8-2
tag:
- bioinformatics
- samtools
- ngs
category: blog
author: dongjo

---
## Background

While examining BAM files generated from a couple years back, I wanted to see if the reads that were aligned to the reference genome was paired-end reads. With some help from <a href="https://www.biostars.org/" target="_blank">Biostars</a> community, I was able to declare that the reads were actually single-end reads.

Note: The reads were from Ion Torrent sequencing machine and they are mostly single-end (found this out a little after checking with below approaches).

## Approaches

### Attempt to gather information from header

@PG of header may contain command line prompt (e.g. CL: XXX) used to generate the .BAM file

{% highlight bash %}

# Retrieve header information using samtools

samtools view -H <input-bam-file> | grep "@PG"

{% endhighlight %}

If we observe useful information, we could stop here. If not, we can proceed to check the bitwise flag for each read in .BAM file.

### Examine the bitwise flags

{% highlight bash %}

# Bitwise flags can be found in the 2nd column in SAM
# Sort and count the number of each bitwise flags present

samtools view <input-bam-file> | cut -f2 | sort | uniq -c

{% endhighlight %}

If the input .fastq file(s) was/were indeed paired-end data, then we should be observing high number of bitwise flags 99 or 147. For bitwise flags and their meanings, refer to this <a href="https://broadinstitute.github.io/picard/explain-flags.html" target="_blank">resource</a> from Broad Institute.

### Additional options

If .BAM was generated from single-end reads, the below line should output 0.

{% highlight bash %}
# -c option will return the count of matching records specified by -f option.
# '-f 1' refers to reads having bitwise flag of 1
# bitwise flag 1 == paired-end

samtools view -c -f 1 <input-bam-file>

{% endhighlight %}

If all of above options don't work for some reason or you want to examine each reads in .BAM on your own:

{% highlight bash %}

samtools sort -n -o <output-sorted-bam-file> <input-bam-file>
samtools view <output-sorted-bam-file> | head -n <num-lines>

{% endhighlight %}