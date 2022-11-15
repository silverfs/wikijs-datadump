---
title: Network Intrusion Detection and Prevention
description: 
published: true
date: 2022-11-15T20:06:53.501Z
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

Installing Suricata doesn't make it work out of the box. I'll have to add interfaces to the Suricata menu to work with them.

![interfaces.png](/bok/nids/interfaces.png)