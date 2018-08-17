---
title: "A quick check for Phred score encoding for a .fastq file"
layout: post
date: 2018-5-30
tag:
- bash
- linux
- bioinformatics
category: blog
author: dongjo
---

## Background

One of many ways of examining Phred score encoding for a .fastq file. The code below only checks to see if the encoding is Phred+33 (Sanger, Illumina 1.8+).

## Approach

{% highlight bash %}

# Check every 4th line in the .fastq file
# Examine first 10,000 lines
# Look to see if ASCII characters that do not belong in Phred+33 encoding is present
awk '{ if (NR%4==0) print($0); }' <fastq-filename> |\
head -n 10000 |\
grep -E '([JKLMNOPQRSTUVWXYZ\^_\`abcdefghi]|\[|\])'

# If any lines are returned, then the encoding is not in Phred+33.

{% endhighlight %}