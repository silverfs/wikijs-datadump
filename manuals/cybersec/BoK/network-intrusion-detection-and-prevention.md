---
title: Network Intrusion Detection and Prevention
description: 
published: true
date: 2023-01-09T15:22:07.836Z
tags: 
editor: markdown
dateCreated: 2022-11-08T15:26:58.120Z
---

# Overview
An intrusion detection system (IDS) is a device or software application that monitors a network or systems for malicious activity or policy violations. The most common classifications are network intrusion detection systems (NIDS) and host-based intrusion detection systems (HIDS).


# Differences
- **NIDS**
Network Intrusion Detection System (NIDS) is a type of security software that monitors network traffic for signs of security breaches or malicious activity. It analyzes network traffic in real-time to identify patterns or anomalies that may indicate an attack or compromise. NIDS is typically deployed at strategic points within a network to monitor traffic for all devices on the network.
<br />

- **HIDS**
Host-based Intrusion Detection System (HIDS) is a type of security software that monitors and analyzes activity on a single host or device for signs of security breaches or malicious activity. It analyzes logs, system files, and other data sources on the host to identify patterns or anomalies that may indicate an attack or compromise. HIDS is typically installed on individual devices or servers to monitor activity on those specific devices.
<br />

- **IDS**
Intrusion Detection System (IDS) is a general term that refers to any system that is designed to detect security breaches or malicious activity within a computer system or network. IDS can be either network-based (NIDS) or host-based (HIDS), as described above.
<br />

- **IPS**
Intrusion Prevention System (IPS) is a type of security software that is designed to actively block or prevent security breaches or malicious activity. It analyzes network traffic in real-time, like a NIDS, but also has the ability to take proactive measures to prevent attacks or compromise. This may include blocking traffic from a specific IP address, closing a network port, or quarantining a file. IPS is typically deployed in a network to actively protect all devices on the network.

<br />
<br />

[Source 1](https://fhict.instructure.com/courses/12541/pages/reference-host-intrusion-detection-and-prevention-hids?module_item_id=838305) 

<br />
<br />

## Suricata




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

This category has rules about ICMP requests. Enabling these rules allows suricata to register pings as alerts.
There are more rules, but I'll not touch them for now.

At this point, my router crashed. I successfully rebooted but couldn't start up Suricata on my WAN connection. Removing the rule category didn't help either. I tried changing from vmnet and eventually reinstalled suricata, but to no avail.
The guide was a big help, but even without it, I learned a lot about Suricata and how to set it up. Watching some videos showed how to successfully deply an IDS on a router and how to use it to monitor and block IPs. I contacted a classmate and we discussed the Suricata deployment. I will try to continue later when I have some time left, until then, I will focus on other assignments.


<br />
