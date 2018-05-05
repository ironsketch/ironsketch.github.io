---
layout:     post
title:      OS GetTime.c
date:       2018-02-06
summary:    Summary - Lab7 in Operating Systems has been fun. I really enjoy modding and dividing But here is my silly little get time function... Unfortunately I am either wrong in getting the time or the server this runs off of is wrong. I will assume I am wrong.
permalink: /oslab7gettime/
categories: bash script curl os161 binary search tree c++ iterator c sys161 cscope const pointers references operating system programming programmer female computer science ghci haskell
---

Lab7 in Operating Systems has been fun. I really enjoy modding and dividing : D But here is my silly little get time function... Unfortunately I am either wrong in getting the time or the server this runs off of is wrong. I will assume I am wrong.

{% highlight c %}
/* Getting time
 * Michelle Bergin
 */

#include <unistd.h>
#include <stdio.h>
#include <time.h>

// 31540000
// 2628000
// 86400
// 3600
// 60
// 1

int main(){
	time_t t;
	time(&t);
	int start;
	start = t;
	int year = (start / 31540000) + 1970;
	start = (start % 31540000);
	int month = start / 2628000;
	start = (start % 2628000);
	int day = start / 86400;
	start = (start % 86400);
	int hour = start / 3600;
	start = (start % 3600);
	int minute = start / 60;
	start = (start % 60);
	int second = start;

	printf("test %d/%d/%d %d:%d %d seconds\n", year, month, day, hour, minute, second);
	return 0;
}
{% endhighlight %}
