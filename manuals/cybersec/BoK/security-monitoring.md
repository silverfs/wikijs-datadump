---
title: IT Security Monitoring
description: 
published: true
date: 2022-12-04T20:21:35.645Z
tags: 
editor: markdown
dateCreated: 2022-12-02T12:22:54.618Z
---

# The Basics
IT Security Monitoring, and network security monitoring, enable SIEM for SOC by integrating sensors, logging facilities and business rules or policies into smart detection of threats in the IT environment. In this document, I'll be installing Zeek; an opensource security monitoring sensor.

<br />

# Installation of Zeek

Zeek will be installed on a 20.04 Ubuntu server VM. The provided documentation from school is broken, so I'll use an alternative method. 

I made sure my system was updated and then proceeded to add the Zeek repository to my machine by running these commands seperately.

```bash
echo 'deb http://download.opensuse.org/repositories/security:/zeek/xUbuntu_20.04/ /' | sudo tee /etc/apt/sources.list.d/security:zeek.list
```

```bash
curl -fsSL https://download.opensuse.org/repositories/security:zeek/xUbuntu_20.04/Release.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/security_zeek.gpg > /dev/null
```

```bash
sudo apt udpate
```
<br />

I then checked if it was correctly displayed and which version of Zeek I'll be installing:
![cache-policy-zeek.png](/bok/sec-mon/cache-policy-zeek.png)

Next, I installed zeek using 
```bash
sudo apt install zeek
```

By default, zeek will install itself under `/opt/zeek`. We will have to add the Zeek binary path to PATH:

```bash
echo "export PATH=$PATH:/opt/zeek/bin" >> ~/.bashrc
```

```bash
source ~/.bashrc
```

<br />
<br />

Now that we got Zeek properly installed, we start by beginning to monitor the local network. To do that, we'll have to specify which network Zeek listens to.
```bash
sudo nano /opt/zeek/etc/networks.cfg
```

Inside the file, there are 3 default networks defined. I'll add mine below the 3 and save the file afterwards.
![zeek-networks.png](/bok/sec-mon/zeek-networks.png)

<br />

Let's configure our Zeek cluster for our VM:
Open `sudo nano /opt/zeek/etc/node.cfg` and change the interface for your VM. 
The same for `/opt/zeek/etc/zeekctl.cfg` where I enlarge my log rotation interval to 86400 seconds so I can view more of my logs.

<br />

---

Let's start up zeekctl by running `check` from `opt/zeek/bin/zeekctl`:
![zeek-check.png](/bok/sec-mon/zeek-check.png)

<br />

Deploy Zeek using:
![zeek-deploy.png](/bok/sec-mon/zeek-deploy.png)