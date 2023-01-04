---
title: Network Scanning and Enumeration
description: 
published: true
date: 2023-01-04T23:37:20.559Z
tags: 
editor: markdown
dateCreated: 2023-01-04T23:37:20.559Z
---

# Introduction
This article will talk about the basics of network scanning with Nmap.

There are different kinds of port scan techniques.

<br />


**TCP SYN**
A TCP SYN scan is a populair scan because of it's quick and easy deployment. They also don't get blocked by firewalls that easily. It is a type of network scanning technique used to determine which ports on a target host are open. It works by sending a TCP SYN packet to the target port and waiting for a response. If the target port is open, it will respond with a TCP SYN-ACK packet. If the target port is closed, it will respond with a TCP RST packet. By analyzing the responses, an attacker can determine which ports are open on the target host and potentially use this information to launch further attacks. Below is a visualization of the actions taken in a SYN scan.

![1.png](/bok/enummeration/1.png)

<br />

The reason why it is kind of hidden is because it never completes the TCP connection. You could still be detected, because it is still TCP/IP traffic, which always has to have a sender where the SYN response has to return to.

<br />

---

<br />

This was an example of TCP scanning, but of course not every service runs on TCP. Services like DNS, DHCP and SNMP make use of UDP. unlike TCP, UDP is a connectionless protocol, which means that it does not establish a connection before sending data. This makes UDP scanning slightly more difficult than TCP scanning, as the attacker cannot rely on a connection being established in order to determine if a port is open or closed. 

UDP scans are a lot slower and more difficult, and many mistakes can be made with UDP services. When you start a scan, you'd send empty UDP-packets. However, at some common ports like `53`, `161` and `123`, protocol-specific packets are used in traffic. Ports can give a reaction more often in some cases. One of the biggest turn-downs is playing the waiting game. In a UDP scan, it is more difficult to determine which ports are open, as the host may not send a response at all. This can result in false positives or false negatives, which can make the scan take longer. There are a total of 65,536 ports, which would take hours to scan. Default scans in Nmap do the 1000 most common ports. Still, it has it's positives, despite the long waiting.

<br />

---

<br />

I'll perform a scan on a Windows server from a ubuntu machine as followed:

```
sudo nmap -v -sS 192.168.2.2
```
And these are the results. You can observe the ports that are open and can recognize them, like `53` for DNS.

![2.png](/bok/enummeration/2.png)

<br />

Now we know what ports are open, but it would be nice if we'd know what version of what service is running behind the ports. The parameter `-sV` detects the version of the service. You can also adjust the intensity of the scan with `--version-intensity` which can be set from 0 to 9. The higher the intensity, the more likely the scan will succeed, but the scan will take longer. By default, the intensity 9 is used. 
For now, we use the following command: 

```
sudo nmap -sV 192.168.2.2
```

And here are the results this time:

![3.png](/bok/enummeration/3.png)

A lot of services have been recognized. Although one service couldn't be recognized. 

---

Guessing the OS of a target is also an option. Well, there are a few options. `--osscan-limit` 
<br />
<br />