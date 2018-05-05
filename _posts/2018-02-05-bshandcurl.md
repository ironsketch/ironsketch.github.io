---
layout:     post
title:      Bash and Curl
date:       2018-02-05
summary:    Summary - For our Networking class we are learning about SYN flood attacks. So we have a bunch of VMs set up. On our client side we need to create a bash script that uses CURL to request the server once every second. It was fun to make
permalink: /bshandcrl/
categories: bash script curl os161 binary search tree c++ iterator c sys161 cscope const pointers references operating system programming programmer female computer science ghci haskell
---

For our Networking class we are learning about SYN flood attacks. So we have a bunch of VMs set up. On our client side we need to create a bash script that uses CURL to request the server once every second. It was fun to make:

{% highlight bash %}
#!/bin/bash
COUNTER=0
while [ $COUNTER -lt 60 ]; do
	sleep 1
	curl 192.168.3.138 > /dev/null 
	let COUNTER=COUNTER+1 
done
{% endhighlight %}

Simple but I am happy!

{% highlight ascii %}
  /\_/\
 ( o.o )
  > ^ <
{% endhighlight %}
