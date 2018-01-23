---
layout:     post
title:      Learn me a Haskell
date:       2018-01-22
summary:    Chapter 1 in Learn me a Haskell for Great Good
permalink: /learnmeahaskellch1/
categories: programming programmer female computer science ghci haskell
---

We aren't learning Haskell in class but I want to learn. So I got the book, Learn You a Haskell for Great Good! I have finally finished CH1. Which doesn't sound like much but when you are as busy as I am, it's a great feat! 

Also I have moved my site to github so I am learning how to use their syntax with jekyll.

{% highlight haskell %}
trip = [(a,b,c) | a <- [1..10], b <- [1..10], c <- [1..10], a+b+c == 24, a^2+b^2==c^2]
{% endhighlight %} 
