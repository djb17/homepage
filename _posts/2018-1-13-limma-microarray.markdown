---
title: "Reason for log2 transformation for microarray data before performing limma analysis"
layout: post
date: 2018-1-13
tag:
- limma
- microarray
- R
category: blog
author: dongjo

---

## Background

<a href="https://stackoverflow.com/questions/16864941/python-count-items-in-dict-value-that-is-a-list" target="_blank">limma</a> for microarray analysis

## Explanation from the documentation

"...expression values are more nearly normally distributed and homoscedastic on the log-scale, hence taking means on the log-scale is <u>statistically more powerful and less influenced by individual arrays</u>."

Homoscedatic: having similar variance between samples from the regression line.