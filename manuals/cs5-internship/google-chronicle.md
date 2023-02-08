---
title: Google Chronicle
description: 
published: true
date: 2023-02-08T12:42:53.919Z
tags: 
editor: markdown
dateCreated: 2023-02-08T09:15:41.241Z
---

# Introduction
This page will help in understanding Google Chronicle as best as possible in a short amount of time.

<br>

# What is it?
[Google Chronicle](https://chronicle.security/) is a scaled, cloud-native security analytics platform for threat investigation and hunting. Google Chronicle is built for managing an incredible amount of data in an efficient manner within an enterprise network. 
It provides many benefits over other solutions, like threat detection at Google speed and scale through Intelligence data fusion and indexing via Google. This provides a clear monitoring overview. 


# Data Collection
Chronicle ingests different types of security data and telemetry types through a variety of methods. It uses a *Forwarder*: a lightweight software component, deployed in the customer's network. The *Forwarder* supports syslog, packet capture and existing log management or SIEM data repositories. It uses Ingestion APIs that enable logs to be sent directly to the chronicle platform, eliminating the need for additional hardware or software in customer's network environments. Below is a diagram that shows how data would be sent and collected.
<br>

<img src="/cs5/chronicle/chronicle-data-flow.png" width="800"/>

<br>
<br>

In short: The *Forwarder*  

## Intelligent Data Fusion
Chronicle is able to map logs into a common model that enriches them automatically and categorizes them into timelines. This helps in displaying the entire span of an attack, which makes investigation efforts more easy and effective. 





<br>

# Collecting and parsing data
Parsing log varianats for normalizing data. 



<br>

# Used Terms
- SIEM: Security Information Event Management
- IOC: Inicator of Compromise
- IOA: Indicator of Attack


<br>
<br>

# Sources

- [Google Chronicle Documentation](https://cloud.google.com/chronicle/docs/overview)
- [Google Cloudskillsboost](https://www.cloudskillsboost.google/)