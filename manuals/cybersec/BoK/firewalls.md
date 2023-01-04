---
title: Network Seperation and Segmentation
description: 
published: true
date: 2023-01-04T15:33:42.176Z
tags: 
editor: markdown
dateCreated: 2023-01-02T20:29:10.329Z
---

# Introduction

In this assignment I have to build a network that has a router with 2 firewalls. One firewall is for the DMZ the other one is for the LAN network. This is a very common method of setting up a DMZ to host servers that need to be available to users outside the network. This concept is used worldwide by organizations or individuals hosting online services.

I created this network in VMWare Workstation. I began by creating a PFSense router with 3 network cards (WAN, LAN, DMZ). The DMZ has an NGINX webserver on an Ubuntu server. The LAN side has a Windows client and a Windows Server 2016. 

<br />

This is how the network looks like.

![networkdrawing.png](/bok/firewalls/networkdrawing.png =x450)

<br />

This network diagram shows 3 firewalls: one for each network endpoint. The WAN connection ensures a connection to the internet. The LAN interface is on the `.2` network, and has a subnet of `/24`. In our case, enough clients can connect within this network. The DMZ is on the `.3` network, and has a subnet of `/30`, which means that only 2 usable IP addresses are present. one of them is for our webserver. This ensures Man In the Middle attacks are not possible in this network because there'll be no other IP addresses to give.

![1.png](/bok/firewalls/1.png)

<br />

Using a simple firewall configuration in my DMZ, rules exist that all incoming traffic is allowed on port 80 and 443 on 1 IP address, that being the webserver. All devices within the DMZ have access to everything outside of the DMZ network. Ports will be managed here.

![2.png](/bok/firewalls/2.png)

This way, I've made sure the webserver is available on the networks where needed.


![9.png](/bok/firewalls/9.png)

<br />

I've configured the DHCP server on my lan network like so:

![3.png](/bok/firewalls/3.png)

The DNS server is configured to be set on the Windows server, so clients can connect to to the domain of the domain controller.

<br />

---

<br />

For the domain controller, I began by setting up a static IP address, so I know to always see my server on this address. 

![7.png](/bok/firewalls/7.png)

From there, I started on the domain controller. First made a name for the server and then proceeded to create a root domain: `silver.com`. It will function as an active directory domain controller that will manage clients. I can do more things like policies for safety

![4.png](/bok/firewalls/4.png)

When everything was set up, the server was successfully converted to a domain controller.

![8.png](/bok/firewalls/8.png)

Next, I've added a domain user to my domain so my Windows client can login through the domain. 

![5.png](/bok/firewalls/5.png)

To be able to login with a domain user, I have to add the client to the domain as well. 

![6.png](/bok/firewalls/6.png)

<br />

Now, everything's connected on the network and domain with proper segmentation. Interfaces use rules appropiate to their functionality.

