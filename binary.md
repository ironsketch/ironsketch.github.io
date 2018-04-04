---
layout: default
title: Binary Exploitation
Permalink: /binary/
---

### Binary Exploitation ###

##### 04/04/2018 #####

Yesterday I started working on Modern Binary Exploitation bomb problems. I have already finished all crackme's last quarter and had started on ./bomb. But I found it very hard. Yesterday I saw that there was a second bomb exploit, ./cmubomb. So I started on that and got the first phase done.

Here is what I noticed. 

* I noticed that there seemed to be an argument passed to main. Which usually only happens if you are passing in a parameter.
* I saw thar there was 2 logic branches. One asking if there was one argument passed, and another asking for two. 
* I then passed cmubomb a file I aptly named, butts and it took it. 
* Then I used radare to search the binary. I found phase_1 and opened the function with (s sym.phase_1) I noticed a phrase, "Public speaking is very easy." 
* I put this phrase in my butts file and ran the cmubomb and got through phase 1!!

Now I am trying to get through phase_2. Again I ran through radare and I am finding a function that is called after phase_2 is called but seemingly before phase_2 is run. It's sym.read_six_numbers. I tried using GDB to see what is happening because I am getting confused but I get a segmentation fault at this point... :/ So here is what I am noticing:

###### Phase_2 ######

* It's moving what's passed through by arg_8h to edx
* Then there is this weird thingy that I need to ask David about: add esp, 0xfffffffffffffff8
* Then there is this thing with a local variable: lea eax, [local_18h] I'm confused by lea. I know it's an arithmetic operator for higher bit calculations or something like that but I... am... confuzzled

###### read_six_numbers ######

* Phase_2 then jumps to this function where it fails... But it fails before (or so I think) it even gets to the comparison. I am a bit stuck. I need help at this point.
