---
layout:     post
title:      Data Structures Search BST function
date:       2018-01-25
summary:    I'm proud of my little search function
permalink: /dslab3search/
categories: data structures bst binary search tree c++ cpp compile os161 c sys161 cscope operating system programming programmer female computer science ghci haskell
---

I made a search function for my binary search tree. I don't know if it will always work. I emailed the teacher for feedback. But I am quite proud regardless.
Binary Search Tree
{% highlight c %}
bool search(const Obj &x){
            return search(x, root);
        }
        bool search(const Obj &x, bstNode *&n){
            if(n == NULL){
                return false;
            } else {
                return search(x, n->left) || (x == n->data);
                return search(x, n->right) || (x == n->data);
            }
        }
{% endhighlight %} 

