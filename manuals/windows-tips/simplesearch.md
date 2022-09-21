---
title: Simple Search
description: 
published: true
date: 2022-04-17T22:31:09.515Z
tags: privacy, windows, search, regedit
editor: markdown
dateCreated: 2021-08-31T09:21:34.652Z
---



Not many people ... with a good functioning searchability. No matter on what platform or service, be it a searchengine or an operating system, your results are best unfiltered, uncensored and untracked.
Unfortunately, we can't be 100% free of those shackles, but we still have our choices. Simple Search may be your first step to a better Windows experience... 


## Simplified searching on Windows 10
The searchbar in Windows 10 can be either nice to use or incredibly irritating.
Let me give you an example.

In most cases, your Windows searchbar would look like this:

<img src="/simple-search/download.jpg" width="800"/>

</br>

Of course, we want to get rid of this. We don't want to see best matches and accidentally click on a webpage again. 
To do this, execute these following three commands in a command prompt:
```bash
reg add HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Search /f /v BingSearchEnabled /t REG_DWORD /d 0
reg add HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Search /f /v AllowSearchToUseLocation /t REG_DWORD /d 0
reg add HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Search /f /v CortanaConsent /t REG_DWORD /d 0

```

These commands add 3 keys in your Windows Registry. One Disables Bingsearch in the searchbar. The second one disables the use of your location when using the searchbar to search for stuff. The last one retracts the use of Cortana in the search function.

