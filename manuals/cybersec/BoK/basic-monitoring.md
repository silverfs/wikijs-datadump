---
title: Basic Monitoring
description: 
published: true
date: 2023-01-08T23:04:00.892Z
tags: 
editor: markdown
dateCreated: 2023-01-08T23:04:00.892Z
---

# Introduction

In this article, I'll conduct some experiments setting up Zabbix as a monitoring server. 
I have a little experience using Zabbix, as I've worked with it before on a past internship.
<br />

# Installation

I will install Zabbix on an Ubuntu 22.04 server  with MySQL and Apache as webserver.
I will follow the default installation instructions on Zabbix [here](https://www.zabbix.com/download?zabbix=6.2&os_distribution=ubuntu&os_version=22.04&components=server_frontend_agent&db=mysql&ws=apache).
The installation is pretty straightforward, so I won't be documenting that part.

<br />

---

The installation went rather well. I did came accross an issue where I couldn't connect my Windows Server 2016. Everytime I tried adding the server, it kept giving me a down signal. Turns out I've accidentally filled in the wrong port number. But, all in all, the process went smooth.


![1.png](/bok/monitor/1.png)