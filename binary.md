---
layout: default
title: Binary Exploitation
Permalink: /binary/
---

### Binary Exploitation ###

##### 04/09/2018 #####

I was working on the lab.zip from the website but I was told to do the ones from warzone. That made my life a LOT easier. I solved the lab1C in about 5 minutes.

###### lab1C ######

* I first ran ./lab1C to see what would happen. As I assumed it wants a password.
* I then opened up radare with r2 ./lab1C
* I ran aaaa, went to main with s main, and then looked at the visual with VV. 

When using scanf the right most input will be the string and the left is the string format. So I could tell that since data is put in from right to left that my input would be local_1ch. With that info I am looking at this little section:

![alt text](http://intmain.in/images/lab1C.png "lab1C")

* I see that my input is being moved into eax and then compared to 0x149a
* I then decide to check out the list view of what is going on in radare2 with the command pdf
* I noticed that the string format is %d so I decided to get the numerical value of that hex which is 5274
* I submitted that as the password and got authenticated!

##### 04/08/2018 #####

For Modern Binary Exploitation I am also reading the book: Hacking the Art of Exploitation by Jon Erickson [https://nostarch.com/hacking2.htm](https://nostarch.com/hacking2.htm) I have finally finished CH2. Chapter 3 is about exploitation where 1 and 2 were about the C language. I read it all because my assumption is that this author will focus on teaching me specifics about the C language that can be exploited. 

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
