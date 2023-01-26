---
title: What is Docker Swarm?
description: 
published: true
date: 2023-01-26T17:23:46.243Z
tags: docker, guide, manual, virtualization, swarm
editor: markdown
dateCreated: 2021-08-21T22:26:03.142Z
---

## Clustering
Docker Swarm is a tool that "clusters" many Docker Engines and schedules containers. Docker Swarm decides which host to run the container based on your scheduling methods.

Let's say you have a couple of Docker hosts. each host, has their own Docker Deamon. The swarm manager will connect each and every Docker Deamon based on your discovery method. The Swarm manger then knows the status of every host in the cluster. If you decide to run a container, the Swarm manager will decide on which container it runs. The work load will be divided by the "work nodes" in the swarm and is transparent to the end users.

So, basically, Docker Swarm can group multiple hosts into a cluster and distribute docker containers among these hosts.

![docker-swarm-exp.png](/docker/swarm/docker-swarm-exp.png)