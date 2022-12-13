---
title: Secure Remote Access and Management (VPN)
description: 
published: true
date: 2022-12-13T21:53:57.755Z
tags: 
editor: markdown
dateCreated: 2022-12-12T15:35:51.836Z
---

# Introduction
In this document, I'll be creating a VPN server on my network so I can access my internal network through the WAN connection.

# Config

I will be using the OpenVPN Wizard with local user access, because it's a straight forward process.
I'll also use a key length of 4096 for extra security. 

![1.png](/bok/vpn/1.png)

I'll also need to add a server certificate. I'll use the same configuration here, Including the 4096 key length.

![2.png](/bok/vpn/2.png)

After this, I configure the OpenVPN service myself. I let it generate a TLS key for authentication so the server knows to connect the right client, of course using a 4096 bit key.

My local network is `192.168.2.0/24` and I'll use `10.0.10.0/24` for my tunnel network.
I also set up my router IP `192.168.2.1` as my DNS server for distributing IPs.
![3.png](/bok/vpn/3.png)

I'll enable all options in the next step to automatically generate rules.

![4.png](/bok/vpn/4.png)

---

Now that the configuration is finished, I'll create a user to connect with.

![5.png](/bok/vpn/5.png)

I'll also create a certificate for this user using the OpenVPN client export package. 

![6.png](/bok/vpn/6.png)

---

<br />

## Test

The only thing left to do is to install the OpenVPN client on a Windows machine. I installed the OpenVPN Client provided from the router and connected with my `silver` user credentials. It worked!

![7.png](/bok/vpn/7.png)

This log from the client shows a successful connection to the router.
<br />

Doing an `ipconfig` on the Windows client machine reveals an extra network adapter which OpenVPN uses to connect to the correct tunnel. And that seems to work as well!

![8.png](/bok/vpn/8.png)

Pinging the other network from the Windows client doesn't seem to be a problem as well.

![9.png](/bok/vpn/9.png)
<br />