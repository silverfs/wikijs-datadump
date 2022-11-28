---
title: Network Intrusion Detection and Prevention
description: 
published: true
date: 2022-11-28T22:23:47.147Z
tags: 
editor: markdown
dateCreated: 2022-11-08T15:26:58.120Z
---

# Overview
An intrusion detection system (IDS) is a device or software application that monitors a network or systems for malicious activity or policy violations. The most common classifications are network intrusion detection systems (NIDS) and host-based intrusion detection systems (HIDS).

In this document, I'll install an IDS system on a pfSense firewall. The name of the package is [suricata](https://suricata.io/).
<br />


After making sure my pfSense was up-to-date, I installed suricata using the Package Manager.

![suricatainstall.png](/bok/nids/suricatainstall.png)
<br />

Installing Suricata doesn't make it work out of the box. I'll have to add interfaces to the Suricata menu to work with them. I'll keep the settings on the default values.

![interfaces.png](/bok/nids/interfaces.png)
<br />

I want to add [Snort](https://snort.org) to suricata, so I'll head over to the global settings and hit the Sort user checkbox. I then used my previously created account and extracted an Oinkmaster code. I also added the latest 2.9 Snort rule filename.

![globalsnortoptions.png](/bok/nids/globalsnortoptions.png)
<br />

To finish it off, I need to update Suricata to and it's settings on the Update tab. 

![snortupdate.png](/bok/nids/snortupdate.png)
<br />

---

<br />
I'll now enable some rules that'll give me an alert with certain detections on functions. For the sake of testing, I'll turn on:

![snort-protocol-icmp.png](/bok/nids/snort-protocol-icmp.png).

There are more rules, but I'll not touch them for now.
![category-rules.png](/bok/nids/category-rules.png)

<br />
