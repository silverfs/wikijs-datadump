---
title: Install Windows 11 Without Needing An Internet Connection
description: 
published: true
date: 2023-08-13T21:23:52.967Z
tags: 
editor: markdown
dateCreated: 2023-08-13T21:23:52.967Z
---

# Introduction
I have you wondering, why do we even need to have a hack for this...
That's just how Microsoft is these days.

Anyway, I'll show you how to evade some stupid implementations using a little trickery!

> Before enthusiastically following this guide, you might want to combine this one with [this guide](/manuals/windows-tips/no-bloat-installation) for an installation of Windows 11 without bloatware.
{.is-info}

<br>

# Steps

Boot a Windows 11 ISO like normal. Once you're on the “Oops, you’ve lost internet connection” or “Let’s connect you to a network” page, use the `Shift + F10` keyboard shortcut to open the command prompt. 
<br>
Once you're in the command prompt, type the following down below and press enter:

```
OOBE\BYPASSNRO
``` 

If I'm correct, your computer should restart automatically. Once it boots up again, follow the process like normal, and when you're on the “Oops, you’ve lost internet connection” or “Let’s connect you to a network” page again, click the “I don’t have internet” and the Accept button (if applicable).

That's it. Goodbye.