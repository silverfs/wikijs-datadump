---
title: Password Cracking
description: 
published: true
date: 2023-01-06T19:06:54.700Z
tags: 
editor: markdown
dateCreated: 2023-01-06T19:06:50.409Z
---

# Introduction

Password cracking is the process of attempting to gain unauthorized access to a computer system or online account by guessing or determining the correct login credentials (usually a username and password). This can be done using various techniques, such as attempting to guess the password using common combinations of letters, numbers, and symbols, or using a list or dictionary of possible passwords. In more advanced cases, password cracking may involve using specialized software and hardware to perform a "brute-force" attack, which involves systematically trying every possible combination of characters until the correct password is eventually found. 

<br />

# How does it work?

Using DVWA and Burp Suite, I'll will demonstrate how a simple brute-force attempt would look like.

Heading to the DVWA brute force page and filling in my credentials, we can head over to Burp Suite to look at the following request:

![1.png](/bok/password/1.png)

Taking a better look at this request, you can see in the first line that my used credentials are being used as parameters. I can send this to the Intruder tool within Burp Suite to perform a Sniper attack on the password parameter. And we'll use brute-force at that!

As for the passwords. I'll make use of the top 100 used passwords, taken from [Wikipedia](https://en.wikipedia.org/wiki/Wikipedia:10,000_most_common_passwords), as taking a list of 10.000 passwords would take too long for now. 

![2.png](/bok/password/2.png)

![3.png](/bok/password/3.png)

<br />

Upon starting the attack, Burp Suite will take it's time trying out each password on the provided list. After it's done, I compared the password lengths and saw that 2 requests had different lengths. One is empty, the other one would be 'password'. Now I know that it would be most likely 'password' as password. Using it does indeed bring me success.

![4.png](/bok/password/4.png)

<br />

---

Preventing basic brute force attacks can be done on multiple levels. One of the better things to do is using a "maximum number of retries" on your input fields. Around 3 - 5 times a time before a 10 to 15 minute waiting time triggers should save a lot already. What we can also copy from the free community version of Burp Suite is implementing a delay in inputs in a field, so it would take longer to completely go through a dictionary. Just make sure it doesn't go at the expense of user experience. Other things that would help the security are methods like 2 factor authentication.


<br />
<br />