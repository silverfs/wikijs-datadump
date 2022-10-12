---
title: Network Sniffing and Spoofing
description: 
published: true
date: 2022-10-12T15:00:17.286Z
tags: 
editor: markdown
dateCreated: 2022-10-10T09:41:45.320Z
---

# What is sniffing?


in cyber security terms, sniffing is the act of intercepting and monitoring traffic on a network. This can be done using network/protocol analyzer tools such as Wireshark, a FOSS application and the most commonly used application for things like sniffing and much more. 
In this document, I will make an attempt to sniff a plain http password using 
Wireshark within my network. Sniffing a network is super easy and I'll show you exactly how to do it!
<br />

## Intercepting plain-text passwords

Using Wireshark, we'll take a look at our network. We'll start by capturing incomming and outgoing traffic on the whole network through our own network-card. We'll immediately be greeted by a load of packets, requests, etc. There's a lot of information we don't need, so why don't we start by filtering on our desired content?

Using the input field at the top, we can filter on `http.request.method == POST`, which will filter on post requests through the HTTP protocol. Mine looks something like this:

![wireshark1.png](/bok/wireshark1.png)
<br />

yours may have less or some more entries, but that shouldn't concern you. 
To test our plain-text password sniffing, we'll be using a test website (and obviously with our private credentials). 
Head over to [testphp.vulnweb.com](http://testphp.vulnweb.com/login.php) or any other test website of your liking, as long as the form is HTTP.
I will use _bruh_ as username and _passwordofbruh_ as password.

When I click on __login__, Wireshark will notice a new entry in my filtered list:

![wireshark2.png](/bok/wireshark2.png)

Now, one of the faster ways to find plain-text credentials in request methods like these is by right-clicking the entry and selecting __follow__ --> __TCP Stream__.
It'll be followed by this screen:

![wireshark3.png](/bok/wireshark3.png)

<br />

Notice from the *host* that we have the right request on our screen.
At the end of the screen, there's an _find_ input field. Simply search for words like: **Username**, **Uname**, **password**, passwd**, etc.

I could easily find my used username in password using this method and shows how easily you can do it to!
![wireshark4.png](/bok/wireshark4.png)