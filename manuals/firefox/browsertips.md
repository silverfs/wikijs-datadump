---
title: Firefox Browser Tips
description: 
published: true
date: 2023-01-26T15:44:24.597Z
tags: 
editor: markdown
dateCreated: 2023-01-26T13:41:45.070Z
---

# Introduction
Firefox is a popular web browser known for its speed, security, and customization options. Whether you're a new user or a seasoned pro, there are always ways to improve your browsing experience. 
In this article, I'll share some tips and tricks for getting the most out of Firefox. From shortcuts and extensions to privacy settings and troubleshooting, I'll cover everything you need to know to make your browsing faster, safer, and more efficient.

<br>
<br>


# Dark Mode Everywhere ✨
Don't like to blind yourself when navigation to a website styled only with the colour `#FFFFFF` as a background? Me neither.
<br>

## Extensions

[Dark Reader](https://addons.mozilla.org/en-US/firefox/addon/darkreader/) is by far the most popular en used 'dark mode' extension on Firefox, if not, any browser at this point.
Not only does it have exceptional performance, it also looks good, and is [open source](https://github.com/darkreader/darkreader)!
You can configure the extension to work on specific websites or turn it of and on completely. There are also other tweaks you can use to further customize how dark reader styles websites, like brightness and contrast levels, but also different filter themes.

This is the only dark mode extension I currently recommend, as it is open source and still regularly updated.
<br>

## Expanding the dark
Sadly, Firefox disables functionality of extensions on some pages, like the ones down below:

- accounts-static.cdn.mozilla.net
- accounts.firefox.com
- addons.cdn.mozilla.net
- addons.mozilla.org
- api.accounts.firefox.com
- content.cdn.mozilla.net
- discovery.addons.mozilla.org
- install.mozilla.org
- oauth.accounts.firefox.com
- profile.accounts.firefox.com
- support.mozilla.org
- sync.services.mozilla.com

This is done to prevent additional functionality on them, modify content, or to block elements. Only WebExtensions are hit by this limitation. This means, extensions like Dark Reader won't work here.
<br>

> Remove domains at your own risk!
{.is-warning}

If you truly want to have dark mode on protected pages, follow the steps below.

1. Head to Firefox and enter `about:config`. Proceed when a warning appears.
2. Copy-paste the following:
```
extensions.webextensions.restrictedDomains
```
3. Edit the string and remove domains like `support.mozilla.org` if you want to keep it relatively safe. 
4. Click on the checkmark.
5. Restart your browser and you should be good to go.

https://www.ghacks.net/2017/10/27/how-to-enable-firefox-webextensions-on-mozilla-websites/

<br>
<br>

# Home page and new tab customization:
https://support.mozilla.org/en-US/questions/1280633
https://www.userchrome.org/how-create-userchrome-css.html