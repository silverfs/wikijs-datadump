---
title: Cool Projects for your needs!
description: 
published: true
date: 2022-08-29T20:46:57.761Z
tags: docker, virtualization
editor: markdown
dateCreated: 2022-08-29T19:42:27.680Z
---

# My Recommendations

I got some awesome recommendations for you all! We'll assume that you are Let's dive right into it.
<br />
<br />

## Portainer-CE

[Portainer](https://www.portainer.io/) is a lightweight service delivery platform for containerized applications that can be used to manage Docker, Swarm, Kubernetes and ACI environments. Meaning: a GUI for your containers, Images, Volumes and more (Super cool!).

<br />

I could tell you how it would look and feel, but you can just look at it yourself!

**Try out the public demo instance [here](http://demo.portainer.io/) 
(login with the username _admin_ and the password _tryportainer_).**

*Please note that the public demo cluster is reset every 15min.*
<br />
<br />

### Installation
Alrighty! Now that you've decided to use this piece of software, we'll need to install it in order to use it. 
Start by creating a volume for Portainer's database:
<br />

```bash 
docker volume create portainer_data
```

Next, simply write the following in your terminal to create a container with the portainer image (adjust to your liking):
<br />

```bash
docker run -d -p 8000:8000 -p 9443:9443 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:2.9.3
``` 

> **Quick notice:**
The second port is used as a secure port. Portainer generates a self-signed SSL certificate to secure your instance. 
If you only require the HTTP port in your instance, remove the ports mentioned and add the folowing port
`-p 9000:9000`
{.is-info}

<br />
<br />

And there you go! That wasn't so bad now was it?
Portainer should now be installed on your server. You can check whether Portainer has been started by running:

```bash
docker ps
```

<br />

*Source code available [here](https://github.com/portainer/portainer).*