---
title: Basic Hacking and Pentesting Process 
description: 
published: true
date: 2023-01-06T15:50:58.627Z
tags: 
editor: markdown
dateCreated: 2023-01-06T15:50:58.627Z
---

# Introduction
Executing a pentest, or Penetration Test, we'll have to look at the following topics:

- Test scope
- Kinds of tests to perform
- Goals of the tests
- When tests will be executed.

<br />

As for other important things that we cannot forget, we'll have to make business agreements, like the processing of confidential data, writing and signing a liability agreement and an escalation method in case anything goes wrong in the pentesting process. So, once the documents like the NDA and the Pentest agreement are listed and ready, we can continue with the next step.


# The Plan

Knowing what the customer wants is of utmost importance. We will have to figure out what the customer wants through questions. Doest the customer want us to test a certain application within the network? Is the customer fine with us receiving a piece of code from the application (aka, white box)? Or do we start from 0 knowledge (black box)? These are all questions that we have to ask carefully during the creation of the contract.

Document from this moment on the necessary tools that you will be using. Plan how you will find and gather information (use things like social media, footprinting, etc.) And that's where we'll begin. 

<br />

The first step is gathering information. As any kind of data may be important for the pentest, and depending on the type of test, we can gather a range of different information types. Start by a manual search using search engines and browse through archives and social media pages, or switch directly to an automation tool like The Harvester. The harvester will crawl on search engines in search of information like emails, names, social-media profiles, and not excluding IP addresses, (sub)domains, etc. 

This is a very important step to ensure that we also scan the correct IP addresses. If we are going to scan the wrong IP address, it won't be entirely ethical, because we are trying to scan or hack into a server that does not belong to our target company.

<br />
<br />

After gathering sufficient information, we can start with the second step. Start by digging through teh IT infrastructure by scanning IP-ranges, important servers like AD-servers, mail, etc., open ports and operating systems. 

<br />

The third step is looking for vulnerabilities. By scanning for open ports and operating systems, we can get a pretty decent overview of possible vulnerabilities. Is there a mailserver present? We can try looking on the network for unencrypted traffic. Located a database? Try SQL injection. You can also look for known vulnerabilites at a CVE website. It is important to check for as many loop holes as possible. Having information about a certain system can help more than you think.


<br />

The fourth step will most likely not be performed by an ethical hacker for around 90% of the time, as this can pose some serious threats to the IT environment. Look out for any damages to working systems and note down found vulnerabilities.

<br />

- [Source](https://fhict.instructure.com/courses/12541/pages/reference-basic-hacking-and-pentesting-proces?module_item_id=838283).

<br />
<br />