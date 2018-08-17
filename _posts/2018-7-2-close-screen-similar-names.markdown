---
title: "Closing multiple screen sessions with similar names"
layout: post
date: 2018-7-2
tag:
- xargs
- screen
- linux
- grep
- awk
category: blog
author: dongjo

---
## Background

Wanted to kill some, but not all sessions of screen. The ones that I wanted to kill happened to have similar names designated with -S option.

## Solution

{% highlight bash %}

# 1. Retrieve all screen sessions
# 2. Use 'grep' to retrieve only desired sessions
# 3. Use 'awk' to print only the session names
# 4. Use 'xargs' to kill the screen with the names from 'awk'

screen -ls |\
grep -e '<insert-pattern-here>' |\
awk 'print $1' |\
xargs -I % screen -X -S % kill

{% endhighlight %}