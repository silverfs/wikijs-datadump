---
title: Network Seperation and Segmentation
description: 
published: true
date: 2023-01-02T20:29:10.329Z
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

