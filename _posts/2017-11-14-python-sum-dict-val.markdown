---
title: "Summing up length of each dictionary values"
layout: post
date: 2017-11-14
image: /assets/images/markdown.jpg
headerImage: false
tag:
- python
- dict
category: blog
author: dongjo
---

## Background

I was storing list of strings as a value to a key in dictionary and needed to sum up the counts of total number of elements in the lists for each key. 

## Approach

{% highlight python %}
# data: our dictionary
# We iterate through the values of each key in dict with data.itervalues().
# Then, we use sum to add up all the counts.

sum(len(x) for x in data.itervalues())
{% endhighlight %}

## Sources
For more detailed explanation and examples, refer to the original Stack Overflow post [here][1].

[1]: https://stackoverflow.com/questions/16864941/python-count-items-in-dict-value-that-is-a-list
