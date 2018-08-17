---
title: "Troubleshooting gzopen64 error during bedtools installation"
layout: post
date: 2018-6-13
tag:
- installation
- troubleshooting
- bedtools
category: blog
author: dongjo

---
## Background

Issue encountered when attempting to install bedtools without root privileges on lab server. In my specific case, this was due to LD_LIBRARY_PATH being defined in .bashrc (pointing to my local libraries instead of system's libraries).


## Solution (worked when the issue was encountered)

1. Find where files that have 'libz.so' as part of their name.

{% highlight bash %}

locate libz.so.*

{% endhighlight%}

{:start="2"}
2. In 'Makefile', find the following line:

{% highlight bash %}
...
export LIBS = -lz
...
{% endhighlight%}

{:start="3"}
3. Change the line found in step 2 to the following:

{% highlight bash %}
...
export LIBS = <path-found-from-step-1> -lz
...
{% endhighlight %}

{:start="4"}
4. Re-compile bedtools.

{% highlight bash %}

make clean && make

{% endhighlight %}

## Related Reference

Similar troubleshooting post discussed in <a href="https://groups.google.com/forum/#!topic/bedtools-discuss/sbJNxy3duXY" target="_blank">Google Groups</a>.