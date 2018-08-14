---
title: "Extracting even/odd rows/columns"
layout: post
date: 2018-2-4
tag:
- R
- selection
category: blog
author: dongjo
---

## Approach

{% highlight R %}

# test: our dataframe
# Use logical vectors to select even/odd rows.

test[c(TRUE,FALSE), ] # will get you the odd rows
test[, c(TRUE,FALSE)] # will get you the odd columns

# Placing '!' in front of logical vector results in odd -> even.

test[!c(TRUE,FALSE), ] # will get you the even rows
test[, !c(TRUE,FALSE)] # will get you the even columns

# Every N-th columns/rows

test[c(TRUE, rep(FALSE,N) ), ] # will get you the N-th rows
test[, c(TRUE, rep(FALSE,N) )] # will get you the N-th columns


{% endhighlight %}

## Sources
For more detailed explanation and other examples, refer to the original Stack Overflow post <a href="https://stackoverflow.com/questions/24440258/selecting-multiple-odd-or-even-columns-rows-for-dataframe" target="_blank">here</a>.