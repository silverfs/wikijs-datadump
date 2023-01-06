---
title: Security Incident Management
description: 
published: true
date: 2023-01-06T21:41:48.947Z
tags: 
editor: markdown
dateCreated: 2023-01-06T21:41:48.947Z
---

# Introduction

In this article, I'll talk a bit about security incident management. I'll work with information provided through Canvas and use an example company to write down a case of incident management. 
<br />

# Steps

- **Step 1: Alert Reception**

The service desk receives a notice of a customer that downloaded a "desktop cleaner" because the a website stated that the customer's PC had a virus. This is of course classified as a security incident by the Service Desk employee immediately. The Service Desk has followed the procedure for this and this requires further investigation.

<br />

- **Step 2: Alert Triage and Prioritization**

**Severity and impact potential**
The first most important thing to do is to categorize the incident. This is most likely a malware case. First line reported that it was done the day prior. Systems are segmented, so the likelihood of spreading is fairly low.

**Prioritization**
The software is downloaded on a work laptop. The operating system can be reset. No further escalation is likely required.

**Role Assignment**
As the severity is rahter low, the service desk can handle this case until the end. The service desk will have to reinstall a new Windows image on the work laptop. 

<br />

- **Step 3: Response**

There will be a technical explanation. A clean install of the Operating system on the laptop will be required. The incident will receive a low priority and will be handed over to the service desk. Further notice will be reported at the SOC where the IDS-system will be inspected to ensure no weird traffic has been communicated on the network/vlan of the customer. There will also be another investigation of the desk pc is infected with malware as well.

<br />

- **Step 4: Close the incident and review**

After the incident has been resolved a review has to be done to determine if further actions have to be taken to minimize the risk of the incident occurring again in the future. A study on the IDS system showed no weird network trafic and no remnant traffic from the malware to the outside world. A seperate investigation will be created to handle online downloads within the company. 
The incident is resolved. 




