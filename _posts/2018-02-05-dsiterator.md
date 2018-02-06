---
layout:     post
title:      BST iterators
date:       2018-02-05
summary:    Creating a Binary Search Tree and implementing iterators 
permalink: /bst_its/
categories: os161 binary search tree c++ iterator c sys161 cscope const pointers references operating system programming programmer female computer science ghci haskell
---

So I have been working for a while trying to create a binary search tree. While some of it was easy and some of my recursive knowledge is coming back, esp with the help of my teacher. What I have trouble with is how to set up what I call (which may be) an object. Where do you put the variables that will define my object? How do I set up my object? Those are the major questions. And so setting up the BST was hard but I got it done. But the iterator was a whole 'nother ball game. I needed a LOT of help from the teacher. I am going to post my code. Before, I will explain what I have learned.

So I need to create a class for my iterator.
I put this in my public area. 

{% highlight c++ %}
public:
	class const_iterator{
{% endhighlight %}
