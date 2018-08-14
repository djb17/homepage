---
title: "Fixing ethernet connection on CentOS7 after installation"
layout: post
date: 2018-2-8
tag:
- CentOS
- Troubleshooting
category: blog
author: dongjo

---

## Solution (worked when the issue was encountered)

ifcfg-etho0 may need to be changed using below commands

{% highlight bash %}

cd /etc/sysconfig/network-scripts
sed -i -e 's/^ONBOOT="no/ONBOOT="yes/' ifcfg-eth0 # change ONBOOT to yes in ifcfg-eth0

{% endhighlight %}