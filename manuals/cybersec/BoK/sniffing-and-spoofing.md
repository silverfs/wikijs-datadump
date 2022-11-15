---
title: Network Sniffing and Spoofing
description: 
published: true
date: 2022-11-15T16:56:51.441Z
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


---


# Spoofing and Man-In-The-Middle attacks?

Spoofing is the act of pretending to be another person or system. In this section, I want to explore ARP spoofing and ARP poisoning a network. ARP is a protocol used by every device in a network. It matches IP addresses with corresponding MAC addresses. I want to use ARP to pretend to be the router on a network to access credentials. 

Using VMware Workstation, I created a network with a Kali Linux machine, 1 client and a router. I will be using this network for spoofing and ARP poisoning. in this network, `192.168.10.254` is the address of the router. Let's get started.
<br />
<br />

I began with opening Ettercap on my Kali device with `sudo ettercap -G` (for the graphical interface). Then, I selected the network interface I wanted to use. In my case, I used `eth0`.

Next, I scanned the network for hosts by clicking on the zoom-button at the top. Ettercap found 3 hosts in my network.

![ettercaphostscan.png](/bok/ettercaphostscan.png)

I then added `192.168.10.2` (the client) as target number 1 and `192.168.10.254` (the router) as target number 2.

![ettercaptargets2.png](/bok/ettercaptargets2.png)
<br />

Now that we have setup these targets, it's time to confuse the different IP addresses in the environment. We'll do this by sending ARP information into the environment. 

![beforesniff.png](/bok/beforesniff.png)

![mitm-attack.png](/bok/mitm-attack.png)
<br />
<br />

We'll start Wireshark next to Ettercap to capture the traffic and monitor the network on eth0. Notice the ARP entries in the network in Wireshark.

![arppoison.png](/bok/arppoison.png)
<br />
<br />

Finally, we can focus on our 2 victims in our network. I want to know the credentials of the router. Target 1 (the client) logs in on the router through it's ip in Firefox. Once target 1 logs in - and because of our man-in-the-middle attack - we can figure out the credentials of the router (target 2). Ettercap displays in the picture below the username and password content of the login-page from the router.

![mitm-success.png](/bok/mitm-success.png)
<br />
<br />

This is an example on how quickly we can select targets, disrupt a network and launching a MITM attack using ARP poisoning and finally do a lot more in the environment using Wireshark, like analyzing packets, communication between devices and servers, session-id's, cookie-values and much more. This specific type of attack is used inside a network and is used after analyzing network traffic of clients and servers.
<br />

## To sum up what we have done:
First, an attacker (me) selects some victim machines. He then launches tools like Ettercap to act like a proxy and begins an attack like ARP poisoning. Once the network traffic is confused and corrupted, he will tpically perform the next step, like playing the man-in-the-middle, which are one of the most common goals with ARP poisoning. 
<br />