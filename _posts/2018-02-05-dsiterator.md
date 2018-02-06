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

Then you need a constructor. Now a lot of this was done by my teacher so I won't be necessarily right on everything that I exlpain but I will try my best.

{% highlight c++ %}
const_iterator(bst &t){
	t.elements->clear();
	t.elements = t.inOrder();
	it = t.elements->begin();
}
const_iterator(list<Obj> *l){
it = l->end();
}
{% endhighlight %}

To use your inOrder list you need to store an actual list somewhere. Now at first I was assuming that you would store it with your iterator class. Which is possible but I don't quite know enough to understand how to do that. From what the teacher was saying that you need to pass in the iterator as a parameter. But that isn't 'normal'. Iterators in c++ only use yourList.begin() and yourList.end() not yourList.end(it). So to solve whatever I just said, you put your list in your bst class. You also create one variable for your iterator class, typename list<Obj>::const_iterator it;

How do the constructors get called? Through your bst class when the user calls it. In your bst class you will set up an end and begin functions. 

{% highlight c++ %}
const_iterator begin() {
	return const_iterator(*this);
}
const_iterator end() {
	return const_iterator(elements);
}
{% endhighlight %}
