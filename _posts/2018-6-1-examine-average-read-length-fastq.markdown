---
title: "Examining average read length with awk in .fastq file"
layout: post
date: 2018-6-1
tag:
- bash
- linux
- bioinformatics
category: blog
author: dongjo
---

## Background

Utilizing format of .fastq files, specifically 2nd line for each read entry which contains raw sequence, to calculate the average length of the reads.

## Approach

{% highlight bash %}

# Initialize 'total' to keep track of total length of reads in .fastq
# 'count' will keep track of number of reads in .fastq
# Compute the length of the raw sequence and add it to the current total length
# Divide the total length by the number of reads to get the average read length.

awk 'BEGIN{ total=0; count=0; } {if (NR%4==2) { total+=length($1); count++; }} END{ print(total/count) }' <fastq-filename>

{% endhighlight %}