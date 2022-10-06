---
title: Secure Network Connections (HTTPS/TLS/SSH)
description: 
published: true
date: 2022-10-06T12:29:39.076Z
tags: 
editor: markdown
dateCreated: 2022-10-03T09:39:20.917Z
---

# Introduction 
<br />

SSL is more commonly known as TLS and is a protocol for encrytping internet traffic and verifying website/server identity. It's the standard technology for keeping an internet connection secure and safeguarding a connection between systems. An SSL certificate is what enables a website to move from HTTP to HTTPS. Essentially, it's a datafile hosted in a website's origin server. They contain the public key and the website's identity and other related information. This public key is used to verify the identity of the website/server. 
<br />

## Creating an SSL certificate
To understand more about an SSL certificate and the process of creating one, let's create on in Linux.
I made this this certificate using OpenSSL and Apache2 within WSL2 Ubuntu 22.04.
<br />

I'll hold back the boring stuff and focus on the certificate stuff. Make sure Apache2 is installed. I've enabled ssl and made it default for Apache. The next thing I did was creating the actual keys:

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
```

the `days` flag sets the expiration date of the certificate. The `keyout` flag specifies the path to the generated key and the `out` flag is for the path to the generated certificate. After this, You'll have to provide some basic information about the website that's used within the certificate. Have a look:


![self-ssl1.png](/bok/self-ssl1.png)
<br />

Next, we'll head overto `/etc/apache2/sites-enabled/default-ssl.conf` or wherever your default Apache configuration is and specify our web-domain and the location of our certificate and key file. Save and reload, and voila!

![self-ssl2.png](/bok/self-ssl2.png)
<br />

And with some indepth information about our self-signed certificate, we've completed our basic self-signed certificate. 
Here is some more data about the certificate.

![self-ssl3.png](/bok/self-ssl3.png)

<br />
<br />

We can even view that our certificate is encrypted with RSA 2048:

![self-ssl4.png](/bok/self-ssl4.png)