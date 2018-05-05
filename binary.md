---
layout: default
title: Binary Exploitation
Permalink: /binary/
---

## Binary Exploitation ###

#### ¤ [**lab1C**](#lab1c) ¤ [**lab1B**](#lab1b) ¤ [**lab2C**](#lab2c) ¤ [**lab2B**](#lab2b) ¤ [**lab3C**](#lab3c) ¤ [**lab3C**](#lab3c) ¤

##### 04/23/2018 

##### lab3C #####

This is a lab for learning how to inject shell code. The first thing I do is try to find out how this program is working and where the weak points are. 
A few things I noticed:

* The username is a global variable
* The password doesn't matter, it will always fail
* The password is passed in as a pointer
* I believe we use one variable for the address and another for the code?
* The buffer for the fgets were bigger than the buffer set up for the strings. 

![alt text](http://intmain.in/images/lab3c2.png)
![alt text](http://intmain.in/images/lab3c1.png)

I noticed that this program uses fgets so I read the man page and it takes a stream. This means that I can create a shell code in a file and feed it to the program. ... I think

**Cont 04/24/2018**

I got help from David (other David) for this one. I was on the right track (kinda). So we need to use one variable for the address and one variable for the shellcode. For the username I knew immediatly that I needed to put the username and then the shell code. I also immediatly realized that when I call this location that I will need to move my pointer to a location after the username. 

Then I needed to get the address of the username. Using Radare2 I found it. I then filled the password buffer until it was full and then repeated this address multiple times so that I wouldn't have to worry about exactly finding EIP. This won't always work but it is a good try because it worked!

```
python -c 'print "rpisec\xEB\x15\x31\xC0\x31\xDB\x31\xD2\xB0\x04\xB3\x01\x59\xB2\x0D\xCD\x80\xB0\x01\x31\xDB\xCD\x80\xE8\xE6\xFF\xFF\xFF\x48\x65\x6C\
x6C\x6F\x2C\x20\x57\x6F\x72\x6C\x64"
print "admin" + "A"*63 + "\x40\x9c\x04\x08\x40\x9c\x04\x08\x40\x9c\x04\x08\x40\x9c\x04\x08\x40\x9c\x04\x08\x40\x9c\x04\x08" '
```

In order to get this to work David showed me the commands needed:

To make the file readable as txt BUT hold my correct hex I needed to use this:

```
sudo bash lab3C.sh > magic
```

To run the program correctly with the file piped in (Also allowing the file to stay open so that we can see the script that is run):

```
sudo cat magic - | ./lab3C
```

![alt text](http://intmain.in/images/lab3c3.png)

##### 04/16/2018 

##### lab2B #####

I required a lot of help on this. I new that I somehow needed to overwrite something but I had no idea what! After talking with David I learned that we are overwriting the EIP (The next instruction to run during the return)

So we ran the program with a looong string to see when it breaks, this didn't work. Later we found out that my program was sigfaulting but my computer wasn't printing out the error message. In order to work this lab I started to use GDB. We found out that it starts to over write our EIP at the letter r from this string:
```
123456789abcdefghijklmnopqrstufvxyz
```
It was segfaulting after the r. So that's where I needed to put the address of the function I wanted to run. I wanted to run shell which in radare I found was at 0x080486bd. 
Using GDB I saw that the argument being passed to shell is grabbed from EBP. In radare I saw that it is offset by 8 bytes. At first I padded my shell address with my argument address by 8 A's. But this was 4 too many. So even though it is off by 8 you only need to write out 4 bytes. 
I got the address of the variable exec_string's contents, "/bin/sh" using radare's command izz which was: 0x080487d0
The final run to win was:
```
r $(echo -e 123456789abcdefghijklmnopqr"\xbd\x86\x04\x08AAAA\xd0\x87\x04\x08")
```
Also note that the addresses are put in in little endian

##### 04/16/2018 

##### lab2C #####

This was a lab to teach us about actually exploitation of a program. The source code was given on purpose so that we can see how a buffer overflow works. In the program 
```
int set_me = 0;
char buf[15];
```
Becuase there is no bounds checking, although the buffer is set at 15 the more characters I enter will then start to fill up set_me. I knew this pretty much right away. What I didn't know how to do was complete the comparison in order to get to the password. set_me is compared to 0xdeadbeef which in decimal is 3735928559. So I need my input to be that number when put into set_me. I tried a LOT of ideas, learned about using the escape character. In the end the answer was: \xef\xbe\xad\xde

You had to escape the raw bytes of deadbeef and do it in little endian 

But if you submit it just in command line as is, you will be passing the literal so instead you need to use the echo command with the $() to run a command.
```
./lab1C $(echo -e  AAAAAAAAAAAAAAA"\xef\xbe\xad\xde")
```

##### 04/11/2018 

THIS WAS HARD!!! I again used radare2 and gdb to help me solve this puzzle. Thanks to David and Lucien!

##### lab1B #####

* Running through lab1B in radare2 I noticed a function test. (To jump to a function type ':' then 's sym.functionname' or some variation you'll see)
* Going to test I noticed that this function was taking the text 1337d00d and subtracting my password from it and comparing it to hex 0x15 which is decimal 21. My first thought was that I needed to find out what the decimal form of 21 - from the decimal form of 1337d00d. I found out that it was 322424824 and that in hex is 0x1337cff8. That succesfully passed that test. 

![alt text](http://intmain.in/images/lab1B.png "lab1B")

* This wasn't the solution though! I still got Invalid Password!
* At this point I realize that although using strings in the console for lab1B (strings lab1B) I saw that string 'Invalid Password!' But I couldn't see it in radare2
* After talking to David I learned that you can use izz in radare2 to see strings and associated addresses. This string was located at: 0x08048d1c
* Then I remembered there is a way to find where this address is referenced. To do that type, 'axt @ 0x08048d1c' or in other words 'axt @ addy'
* This was printed out: 

{% highlight bash %}
sym.decrypt; const char * s 0x8048a55 [data] mov dword [esp], str.Invalid_Password
{% endhighlight %}

You will see that the function is referenced here sym.decrypt. We can jump to it with, 's sym.decrypt'
* In here I noticed that if there was a gobbledygook word, 

{% highlight bash %}
Q}|u`sfg~sf{}|a3
{% endhighlight %}

and I saw in radare2 that it was being XOR and in GDB I saw that it was being xor'd with 21 (hex 0x15) 
* My instant thought was that I had to submit text after 322424824 that when XOR'd would equal that gobbledygook. So I quickly did that with python. This did not work. I was headed the right direction but sideways.
* I then decided for fun to XOR the gobbledygook with a number from 1 to the highest ascii number to see what would happen. I stopped the loop for this program when if it equaled the result was Congratulations! And that's what I found! I found out that it can equal that word if XOR'd with 18!
* After talking with Lucien and then taking a break and installing ubuntu and warzone on a google cloud VM instance I went back at it and then it dawned on me! I need to submit a number that when minused from the decimal format of 1337d00d would equal 18! Which is 322424827

I submitted this as the password and got my shell!

![alt text](http://intmain.in/images/lab1B2.png "lab1B2")

##### 04/09/2018 

I was working on the lab.zip from the website but I was told to do the ones from warzone. That made my life a LOT easier. I solved the lab1C in about 5 minutes.

##### lab1C #####

* I first ran ./lab1C to see what would happen. As I assumed it wants a password.
* I then opened up radare with r2 ./lab1C
* I ran aaaa, went to main with s main, and then looked at the visual with VV. 

When using scanf the right most input will be the string and the left is the string format. So I could tell that since data is put in from right to left that my input would be local_1ch. With that info I am looking at this little section:

![alt text](http://intmain.in/images/lab1C.png "lab1C")

* I see that my input is being moved into eax and then compared to 0x149a
* I then decide to check out the list view of what is going on in radare2 with the command pdf
* I noticed that the string format is %d so I decided to get the numerical value of that hex which is 5274
* I submitted that as the password and got authenticated!

![alt text](http://intmain.in/images/lab1C2.png "lab1C2")

##### 04/08/2018 

For Modern Binary Exploitation I am also reading the book: Hacking the Art of Exploitation by Jon Erickson [https://nostarch.com/hacking2.htm](https://nostarch.com/hacking2.htm) I have finally finished CH2. Chapter 3 is about exploitation where 1 and 2 were about the C language. I read it all because my assumption is that this author will focus on teaching me specifics about the C language that can be exploited. 

##### 04/04/2018 

Yesterday I started working on Modern Binary Exploitation bomb problems. I have already finished all crackme's last quarter and had started on ./bomb. But I found it very hard. Yesterday I saw that there was a second bomb exploit, ./cmubomb. So I started on that and got the first phase done.

Here is what I noticed. 

* I noticed that there seemed to be an argument passed to main. Which usually only happens if you are passing in a parameter.
* I saw thar there was 2 logic branches. One asking if there was one argument passed, and another asking for two. 
* I then passed cmubomb a file I aptly named, butts and it took it. 
* Then I used radare to search the binary. I found phase_1 and opened the function with (s sym.phase_1) I noticed a phrase, "Public speaking is very easy." 
* I put this phrase in my butts file and ran the cmubomb and got through phase 1!!

Now I am trying to get through phase_2. Again I ran through radare and I am finding a function that is called after phase_2 is called but seemingly before phase_2 is run. It's sym.read_six_numbers. I tried using GDB to see what is happening because I am getting confused but I get a segmentation fault at this point... :/ So here is what I am noticing:

###### Phase_2

* It's moving what's passed through by arg_8h to edx
* Then there is this weird thingy that I need to ask David about: add esp, 0xfffffffffffffff8
* Then there is this thing with a local variable: lea eax, [local_18h] I'm confused by lea. I know it's an arithmetic operator for higher bit calculations or something like that but I... am... confuzzled

###### read_six_numbers

* Phase_2 then jumps to this function where it fails... But it fails before (or so I think) it even gets to the comparison. I am a bit stuck. I need help at this point.
