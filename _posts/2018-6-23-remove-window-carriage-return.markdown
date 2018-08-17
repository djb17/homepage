---
title: "Replace ^M carriage character with a newline using sed"
layout: post
date: 2018-6-23
tag:
- sed
- linux
category: blog
author: dongjo

---
## Background

Sometimes files contain DOS/Windows carriage return which is annoying when attempting to parse them. If newline isn't being parsed correctly, try the following solution.

## Solution

{% highlight bash %}

# To insert the carriage character, press ctrl+v followed by ctrl+m
# -i option to perform in-place editing
sed -i 's/^M/\n/g' <filename>

{% endhighlight %}