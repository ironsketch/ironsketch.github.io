---
layout:     post
title:      Bash and Curl
date:       2018-02-05
summary:    Creating a Bash Script to Curl to a server once every second 
permalink: /bshandcrl/
categories: bash script curl os161 binary search tree c++ iterator c sys161 cscope const pointers references operating system programming programmer female computer science ghci haskell
---

For our Networking class we are learning about SYN flood attacks. So we have a bunch of VMs set up. On our client side we need to create a bash script that uses CURL to request the server once every second. It was fun to make:

{% highlighting ruby %}
#!/bin/bash
COUNTER=0
while [ $COUNTER -lt 60 ]; do
	sleep 1
	curl 192.168.3.138 > /dev/null 
	let COUNTER=COUNTER+1 
done
{% endhighlighting %}

Simple but I am happy!

  /\_/\
 ( o.o )
  > ^ <
