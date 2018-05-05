---
layout:     post
title:      Plaid CTF Potassium
date:       2018-05-04
summary:    Summary - 
categories: programming ctf pwn exploitation programmer synflood syn attack hack hacker deterlab networking female website bills github
---

From the CTF [plaidctf](https://play.plaidctf.com/) I saw potassium a Pwnable for 800 pts. Obviously it's going to be really hard and I don't expect my self to be able to solve this. But I am going to write down as much as I can to create opportunities for learning.

What it does:

* If you run the program with no parameters it asks you for your name and says hello (what you typed in) 

I ran strings on it so you can guess as to what it does:

* Enter a new message: 
* Gambling mode initiated!
* You rolled a %d. Congratulations %s!
* Hello %s. What would you like to do?
* Invalid command.
* New prompt: 
* Quote of the day: "%s"
* So when I see a couple, I'm like, 'O-K'
* Sorry didn't catch that. Try again?
* Try another one hehe
* You lied about your name? So be it.

There's more but you get the idea.

Using Radare2 I could start to see some of the logic. I need to choose run, debug, or trace. I think I need to use GDB? (brb)
