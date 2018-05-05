---
layout:     post
title:      Data Structures Search BST function try 2
date:       2018-01-25
summary:    Summary - I emailed my teacher for feed back. She said to check if there is a match first... lol which makes a lot of sense. Then to check left and right sperately rather then perusing the WHOLE tree... which also makes a LOT of sense lol. But I still don't know if this is good enough, but I had to add in a check for NULL otherwise I am getting a segmentation fault. I will talk to the teacher tomorrow if I don't feel sick :D
permalink: /dslab3search2/
categories: data structures bst binary search tree c++ cpp compile os161 c sys161 cscope operating system programming programmer female computer science ghci haskell
---

I emailed my teacher for feed back. She said to check if there is a match first... lol which makes a lot of sense. Then to check left and right sperately rather then perusing the WHOLE tree... which also makes a LOT of sense lol. But I still don't know if this is good enough, but I had to add in a check for NULL otherwise I am getting a segmentation fault. I will talk to the teacher tomorrow if I don't feel sick :D 

Binary Search Tree
{% highlight c %}
        bool search(const Obj &x){
            if(isEmpty()){
                return false;
            } else
                return search(x, root);
        }
        bool search(const Obj &x, bstNode *&n){
            if(x == n->data){
                return true;
            }
            if(x < n->data && n->left != NULL){
                return search(x, n->left);
            } else if(x > n->data && n->right != NULL){
                return search(x, n->right);
            } else {
                return false;
            }
        }
{% endhighlight %} 

