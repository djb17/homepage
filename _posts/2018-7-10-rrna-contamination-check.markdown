---
title: "Establishing presence of rRNA contamination - a bioinformatics approach"
layout: post
date: 2018-7-10
tag:
- bioinformatics
- fastqc
- ngs
- rna-seq
- bwa
- rseqc
category: blog
author: dongjo
---
## Background

<div>
	<center>
		<img src="{{site.url}}/assets/images/blog/rRNA_contamination_example.PNG" width="60%"/>
	</center>
</div>
Notice anything strange about per sequence GC content distribution from FastQC? This plot was taken from a FastQC results for RNA-Seq data. From exploring on multiple sources, I narrowed down the possible reasons for GC count per read not following the theoretical distribution and the resulting two peaks:

1. Sequencing quality is poor
2. Contamination (rRNA, adapters, exogenous sequences)

There was no problem with the sequencing quality as quality scores across all bases seemed to be good (> Phred score of 28). I attempted to align the data (using STAR2) and observed a very low % of uniquely mapped reads and relatively high %'s of reads mapping to multiple loci and unmapped reads.

After spending more time on Google, I found two approaches that will help me determine whether there is rRNA contamination in the sample.

In order to make sure that below approaches were working correctly, I downloaded RNA-Seq data for a cell line from GDC's legacy repository as a control and tested them. The results for our control showed that no contamination was present. However, the results for the sample that I was initially analyzing displayed presence of rRNA contamination. 

## Approaches

### Align RNA-Seq reads to rRNA sequences

1. Download rRNA sequences from <a href="https://drive.google.com/file/d/0BweZVB8jfIwPRmt4T2FCRHdzdTg/view?usp=sharing">here</a>. (Thank you <a href="http://genomespot.blogspot.com">Genome Spot</a>)

2. Use an aligner to map the RNA-Seq reads to the rRNA sequences. BWA will suffice.

3. Check resulting SAM/BAM's alignment statistics with samtools flagstat.

### RSeQC

0. Map/Align RNA-Seq reads to a reference.

1. Download human rRNA bed file from <a href="https://sites.google.com/site/liguowangspublicsite/home/hg19_rRNA.bed" target="_blank">here</a>. You may need to perform liftover to hg38.

2. Run split_bam.py. Please refer to usage <a href="http://dldcc-web.brc.bcm.edu/lilab/liguow/CGI/rseqc/_build/html/index.html#spilt-bam-py" target="_blank">here</a>.

The idea here for RSeQC is that you examine the number of reads falling within the regions that correspond to rRNA specified in the .bed file.

## References

STAR2 <a href="https://groups.google.com/forum/#!forum/rna-star" target="_blank">Google Group</a>, <a href="http://genomespot.blogspot.com/2015/08/screen-for-rrna-contamination-in-rna.html" target="_blank">Blog #1</a>, <a href="http://rseqc.sourceforge.net/" target="_blank">RSeQC</a>