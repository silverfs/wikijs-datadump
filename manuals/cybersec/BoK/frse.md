---
title: Footprinting, Reconnaissance and Social Engineering
description: 
published: true
date: 2023-02-13T10:57:31.616Z
tags: 
editor: markdown
dateCreated: 2022-10-07T09:35:57.156Z
---

# What Is Footprinting?

Footprinting means collecting information about systems and the entities they belong to. Collecting this information might sound hard to do, but can be a a breeze in the right circumstances. You can use various Open-Source Intelligence (OSINT) sources to gather and map public data like social- and mass media, archives and geo-location tools like OSM.

- **Gathering information through social networks**
Social media information gathering is widely used and one of the most straightforward and common practices of footprinting. When you have a target in mind, You'll want to find out as much as possible before thinking about hacking, pentesting, etc. Start by gathering first-layer public information, like the target's (business)name and address, what contact methods they use (email, social-media, etc.) Owner of said-business and closely related co-workers, stocks, and much more. You can further dig into a particular person's social-media accounts and find more private information like a home-address, personal email and phone number and what other services they might use. linking several personal data collections can be beneficial to see when that said person leaves to and from work and find out when nobody is present or when it's busy within a company. you could find a floor-map of the building(s) and gather information about the workplaces and server rooms. 
You can go into much more detail and eventually escalate it to a structured attack, but that is a story for another article.
<br />

- **Search Engines**
When you want to use your hacking skills on, for example, a company - be it for nefarious reasons or pentesting - You'll need to gather information to make the process go as smooth as possible.
You can go from as simple as social media scanning to Google Dorks, which I'm still not sure why these features are still allowed and continued. 
For reference, When you use Google Dorks, you use search strings that leverages advanced search operators to find information that isn’t readily available on a particular website and/or in normal circumstances. 
<br />

- **Network Information Discovery**
You can find information through WHOIS. WHOIS is a widely used internet record listing the owners of a domain. The Internet Corporation for Assigned Names and Numbers (ICANN) regulates domain name registration and ownership. Here Things are written about the ownership of the domain and how to contact said persons. Private information is often left out due to abuse of information. Other information includes, but is not limited to IP addresses. Further web-crawling is encouraged to find purposely hidden pages.

## Example

I'll display a short example of footprinting some people in a large company. Let's pick our target first: Volkswagen of America Inc.
It is quite easy to gather email addresses from people. 

- Mark Addy: Mark.Addy@vw.com
- Micro Panse: Micro.Panse@vw.com
- Catharina Mette: Catharina.Mette@vw.com
<br />

---

<br />

Online archives can be an amazing tool when you need to find (old) information. Extra information you gather when you are pentesting something. Many things online (especially known websites) have a high chance of getting archived.

![nu-nl.png](/bok/nu-nl.png)

<br />

---

<br />

Another way of gathering some interesting information is looking at the `robots.txt` files that many websites use. These files will tell the search engine not to crawl mentioned links and will most likely be hidden. 
These are the contents of the .txt file from the US Pentagon:

```css
Sitemap: /SiteMap.aspx
User-agent: *
Disallow: *captcha*
Disallow: /*Print.aspx
Disallow: /*.axd$
Disallow: /*.exe$
Disallow: /bin/
Disallow: /Bin/
Disallow: /*.bin$
Disallow: /*.dll$
Disallow: /*.ssi$
Disallow: /Error/
Disallow: /Controls/
Disallow: /controls/
Disallow: /Utility/
Disallow: /install/
Disallow: /Admin/
Disallow: /App_Browser/
Disallow: /App_Code/
Disallow: /App_Data/
Disallow: /App_GlobalResources/
Disallow: /Components/
Disallow: /Config/
Disallow: /Documentation/
Disallow: /Install/
Disallow: /Providers/
```

Whitehouse.gov has one too:

```css
User-agent: *
Disallow:

Sitemap: https://www.whitehouse.gov/sitemap_index.xml
Sitemap: https://www.whitehouse.gov/es/sitemap_index.xml
``` 

<br />

 ---
 
<br />

Using tools, we can find out some other interesting things from a website. Let's start with a traceroute:

A traceroute to `fontys.nl` would look somewhat like this (done from a virtual machine):

```c
$ traceroute fontys.nl
traceroute to fontys.nl (18.192.85.207), 30 hops max, 60 byte packets
 1  192.168.10.254 (192.168.10.254)  3.078 ms  3.393 ms  3.315 ms
 2  192.168.164.2 (192.168.164.2)  6.696 ms  6.539 ms  6.702 ms
```
What you see above is that the traceroute is visible untill it reaches my WAN address (`192.168.164.2`). I can only view the route up to a certain point.

Here's the one from `fhict.nl`:

```c
$ traceroute fhict.nl 
traceroute to fhict.nl (145.85.4.20), 30 hops max, 60 byte packets
 1  192.168.10.254 (192.168.10.254)  1.088 ms  1.074 ms  1.156 ms
 2  192.168.164.2 (192.168.164.2)  3.709 ms  3.859 ms  3.824 ms
``` 

<br />
<br />

Personally, I like to use [mxtoolbox.com](https://mxtoolbox.com) to check out things like DNS servers and other domain name activities. Of course, you can also check things out through te command line with `nslookup`. Let's find out some servers of these 2 domains again:

DNS Server `fontys.nl`:

surfnet.nl

DNS Server `fhict.nl`:

combell.net

Emailserver `fontys.nl`:

fontys-nl.mail.protection.outlook.com

Emailserver `fhict.nl`:

fhict-nl.mail.protection.outlook.com
 
<br />

---

<br />

Using a tool on Kali Linux called TheHarvester, I can 'harvest' all kinds of data from a domain or IP on the internet.

Using the following command, I'll try to gather as much as possible from `fontys.nl`. (Not every source is included as they either need an API key or are paid).
```bash
theHarvester -d fontys.nl -b "anubis, baidu, bingapi, bufferoverun, certspotter, crtsh, dnsdumpster, duckduckgo, github-code, google, hackertarget, linkedin, linkedin_links, n45ht, omnisint, otx, qwant, rapiddns, sublist3r, threatcrowd, threatminer, trello, twitter, urlscan, virustotal, yahoo" -l 500 -c
``` 
<br />

> The command above is not a brute force command. Still, a lot of data is gathered. 
Take a look below:
{.is-warning}

<br />
<br />

```bash
[*] Interesting Urls found: 17
--------------------
http://cag.fontys.nl
http://www.fontys.nl
https://adfs2.fontys.nl/adfs/ls/?SAMLRequest=lZJBb8IwDIX%2FSpV7aWhhQNQiMTgMiQ0E3Q67pcWFSK3Txe4G%2F35d2TR2QdoxTr5nvxfHpKuyVrOGj7iFtwaIvVNVIqnuIhGNQ2U1GVKoKyDFudrNHlcq7ElVO8s2t6W4Qm4TmggcG4vCWy4SMV9v0zWM9GBYjAdawiSLRrIoJtE4zKJ%2BOBz2tc6Ku3E2kP298F7AUcsmopVqBYgaWCKxRm5LMpS%2BnPj9USqHahCqSL4Kb9H6Mai5o47MNakg0PuCwl5hkc%2FUw7I7ByUFwpv9jDe3SE0Fbgfu3eTwvF394oAHg9CjxhW5RThxp9EGCMgm73oFVAf5RcK%2Fsrz5zuve4N7g4XZU2eURqYc03fib9S4V0%2FgrYdUZd9N%2FzlMB671mHQfXIvHl%2F5%2Fa9svFxpYmP3uzsrQfcweaIRHsGhDB9EL9XZTpJw%3D%3D
https://adfs2.fontys.nl/adfs/ls/?client-request-id=00760563-3d37-4c09-8c00-a84cd42572cc&username=&wa=wsignin1.0&wtrealm=urn%3afederation%3aMicrosoftOnline&wctx=estsredirect%3d2%26estsrequest%3drQIIAeNisFLOKCkpKLbS1y_ILypJzNHLT0vLTE7VS87P1csvSs9MAbGKhLgEklnLGMxtOX16GFb4XFEtOjOLkTMtP6-kslgvL2cVoxROU_QvMDK-YGS8xSToX5TumRJe7JaaklqUWJKZn3eBReAHC-MiVqDpl7VW9n9rrPaZt2-tiN97f8ZTrPpuwTnpLlWV2gUZgcXFxXmFoR5ZBcnl_hlOZabuZX5hZWZ5KX6hqYEWzv4GtgZWhhPYhCawMZ1iY_jAxtjBzrCLUxKnk25xiRgZGBnoGhrqGpkpGBlaGRpZGZtGHeBlAAA1
https://adfs2.fontys.nl/adfs/ls/?client-request-id=2ad2cd90-6a3b-4a4d-b2b3-472038d67950&username=&wa=wsignin1.0&wtrealm=urn%3afederation%3aMicrosoftOnline&wctx=estsredirect%3d2%26estsrequest%3drQIIAeNisFLOKCkpKLbS1y_ILypJzNHLT0vLTE7VS87P1csvSs9MAbGKhLgEJpy9pGWd5eu1abO7gsW1yoBZjJxp-XkllcV6eTmrGKVwmqJ_gZHxBSPjLSZB_6J0z5TwYrfUlNSixJLM_LwLLAI_WBgXsQJN33LU8kx7krlbQ5Dk5_e_5BhPsernuhcGJqV4JLs4WppFpBVWlvlUBid7JhmnVOUXOZVFmjnnpLlm-Bl6BWS42lpYGU5gE5rAxnSKjeEDG2MHO8MuTkmcTrrFJWJkYGSga2ioa2SmYGRoZWhkZWwQdYCXAQA1
https://adfs2.fontys.nl/adfs/ls/?client-request-id=3ee34da4-2efe-4abd-ac85-e9fb0b7558d2&username=&wa=wsignin1.0&wtrealm=urn%3afederation%3aMicrosoftOnline&wctx=estsredirect%3d2%26estsrequest%3drQQIARAA42KwUs4oKSkottLXL8gvKknM0ctPS8tMTtVLzs_Vyy9Kz0wBsYqEuASW-D62-6e312tN68vf3KURl2Yxcqbl55VUFuvl5axilMJpiv4FRsYXjIy3mAT9i9I9U8KL3VJTUosSSzLz8y6wCPxgYVzECjR9oeS0Vu3T3T6zAvIWaUSdYjjFqp_iZBRQlVxmHJ4ZHhSamlPqYllQYBgV6K3vE5HsnZ1W4W5aEZxd6RYQluppa2llOIFNaAIb0yk2hg9sjB3sDLPYGXZxSuJ01QFehh98t9cs_r3-_oa3HgA1&pullStatus=0
https://adfs2.fontys.nl/adfs/ls/?client-request-id=4b82466f-a6f3-43e3-87a7-2c58d6a676b6&username=&wa=wsignin1.0&wtrealm=urn%3afederation%3aMicrosoftOnline&wctx=estsredirect%3d2%26estsrequest%3drQIIAeNisFLOKCkpKLbS1y_ILypJzNHLT0vLTE7VS87P1csvSs9MAbGKhLgE8t2avD8ve-zcvlwn4tqysm2zGDnT8vNKKov18nJWMUrhNEX_AiPjC0bGW0yC_kXpninhxW6pKalFiSWZ-XkXWAR-sDAuYgWafm1Tgf16r20uy9eF7XRQl2c8xaqfUmiSlp9m6WWunx4Zlp-db-lZEuIalp9cGuwR4BtoHGVhHJah72mSYmJqYGtgZTiBTWgCG9MpNoYPbIwd7Ay7OCVxOukWl4iRgZGBrqGhrpGZgoGZlbGFlbFZ1AFeBgA1
https://adfs2.fontys.nl/adfs/ls/?client-request-id=5a978fca-e2d5-44a7-b2aa-a7b5f2dee436&username=&wa=wsignin1.0&wtrealm=urn%3afederation%3aMicrosoftOnline&wctx=estsredirect%3d2%26estsrequest%3drQIIAeNisFLOKCkpKLbS1y_ILypJzNHLT0vLTE7VS87P1csvSs9MAbGKhLgETvVPj7r6aLnLplXLt36698RsFiNnWn5eSWWxXl7OKkYpnKboX2BkfMHIeItJ0L8o3TMlvNgtNSW1KLEkMz_vAovADxbGRaxA04ubxD3LTVP8O1dOOvL__SeGU6z6fmVpjumWFqHphcXO-h6FhX7FWSYVhvoeaZmmrk6BoUXJASmW2oaJQUZhxbaGVoYT2IQmsDGdYmP4wMbYwc6wi1MSp5NucYkYGRgZ6Boa6hqZKRiYWRlbWBlbRh3gZQAA0
https://adfs2.fontys.nl/adfs/ls/?client-request-id=79910229-005b-4fd9-b896-602cb7fad4af&username=&wa=wsignin1.0&wtrealm=urn%3afederation%3aMicrosoftOnline&wctx=estsredirect%3d2%26estsrequest%3drQIIAeNisFLOKCkpKLbS1y_ILypJzNHLT0vLTE7VS87P1csvSs9MAbGKhLgENJkmVkYz3PTfMS1BZ_uvK-tnMXKm5eeVVBbr5eWsYpTCaYr-BUbGF4yMt5gE_YvSPVPCi91SU1KLEksy8_MusAj8YGFcxAo0_dDesHOqOs0OS7vC7fepf2c4xapv7uyWkeSXbFaebOwU6m0UblhSZplYVJptFpLnVJKs7VGS72lmYF5u7pZRbmtmZTiBTWgCG9MpNoYPbIwd7Ay7OCVxOukWl4iRgZGBrqGhrpGZgoGZlbGFlbFR1AFeBgA1
https://adfs2.fontys.nl/adfs/ls/?client-request-id=ba6c8a53-fe98-469e-bdee-08a27a16d34b&username=&wa=wsignin1.0&wtrealm=urn%3afederation%3aMicrosoftOnline&wctx=estsredirect%3d2%26estsrequest%3drQIIAeNisFLOKCkpKLbS1y_ILypJzNHLT0vLTE7VS87P1csvSs9MAbGKhLgEgrtyds34N89t7zuORVVil71nMXKm5eeVVBbr5eWsYpTCaYr-BUbGF4yMt5gE_YvSPVPCi91SU1KLEksy8_MusAj8YGFcxAo0XWtVAMevw8fdG36YrfflFGQ8xarvaxqQWxhhEBXqnlKelOxSlpYdbpylHxBe5poRUmmYa2lpnG3h4RuSXRWWbGtuZTiBTWgCG9MpNoYPbIwd7Ay7OCVxOukWl4iRgZGBrqGhrpGZgpGhlaGRlbFF1AFeBgA1
https://adfs2.fontys.nl/adfs/ls/?client-request-id=c5052483-cc9d-47e1-93e2-bcccc98fc209&username=&wa=wsignin1.0&wtrealm=urn%3afederation%3aMicrosoftOnline&wctx=estsredirect%3d2%26estsrequest%3drQQIARAA42KwUs4oKSkottLXL8gvKknM0ctPS8tMTtVLzs_Vyy9Kz0wBsYqEuASaVViPzj3z0H3yoz1nTvYf4pzFyJmWn1dSWayXl7OKUQqnKfoXGBlfMDLeYhL0L0r3TAkvdktNSS1KLMnMz7vAIvCDhXERK9D0H4c-9d4p2-y3IrFM8NT3ZKZTrPohyd5RaeleJXkBQYVllRn-KYWFUT6e_iVVlR7l_pkmhckhjhl5RVWphZXZtkZWhhPYhCawMZ1iY_jAxtjBzjCLnWEXpyROVx3gZfjBN6Pp7Ov19ze89QAA0&pullStatus=0
https://adfs2.fontys.nl/adfs/ls/?client-request-id=e33ff25a-6a35-433e-b29f-f43174d9415c&username=&wa=wsignin1.0&wtrealm=urn%3afederation%3aMicrosoftOnline&wctx=estsredirect%3d2%26estsrequest%3drQQIARAA42KwUs4oKSkottLXL8gvKknM0ctPS8tMTtVLzs_Vyy9Kz0wBsYqEuASiPtk_Ns2yc940_4thyU3HmFmMnGn5eSWVxXp5OasYpXCaon-BkfEFI-MtJkH_onTPlPBit9SU1KLEksz8vAssAj9YGBexAk2XmH3hk9Svbo-VsdvFr56cznSKVb_YMkXfJTfPP98rwMipzDewoCTX0N85LyXMoyojKS_cKKvKL8gi0i-3yDjQ1tjKcAKb0AQ2plNsDB_YGDvYGWaxM-zilMTpqgO8DD_4-ieevbP-_oa3HgA1&pullStatus=0
https://elo4.fontys.nl/extern/
https://fontys.nl/
https://fontys.nl/E-maildisclaimer.htm
https://fontys.nl/Over-Fontys/Fontys-Academy-for-the-Creative-Economy.htm
https://signin.fontys.nl/my.policy

[*] No Twitter users found.



[*] LinkedIn Users found: 285
---------------------
[Redacted due to privacy conecerns]

[*] No Trello URLs found.

[*] IPs found: 131
-------------------
18.158.85.187
18.192.85.207
20.61.11.181
34.248.154.179
34.250.155.97
34.254.208.210
40.74.22.195
52.17.33.109
52.19.16.24
52.48.193.98
52.49.7.132
52.49.109.21
52.49.227.205
52.51.95.125
52.51.114.198
52.214.156.60
54.72.169.84
54.76.84.20
54.154.229.188
54.171.26.30
54.171.39.205
54.171.44.49
54.194.82.222
54.194.117.152
54.195.153.131
54.220.70.52
63.34.57.105
63.35.34.110
108.128.178.131
145.85.2.6
145.85.2.7
145.85.2.15
145.85.2.16
145.85.2.17
145.85.2.19
145.85.2.21
145.85.2.24
145.85.2.27
145.85.2.28
145.85.2.30
145.85.2.32
145.85.2.33
145.85.2.34
145.85.2.37
145.85.2.40
145.85.2.44
145.85.2.45
145.85.2.46
145.85.2.47
145.85.2.49
145.85.2.52
145.85.2.53
145.85.2.54
145.85.2.58
145.85.2.64
145.85.2.72
145.85.2.82
145.85.2.83
145.85.2.88
145.85.2.94
145.85.2.96
145.85.2.101
145.85.2.102
145.85.2.109
145.85.2.112
145.85.2.121
145.85.2.124
145.85.2.127
145.85.2.129
145.85.2.131
145.85.2.136
145.85.2.137
145.85.2.138
145.85.2.140
145.85.2.141
145.85.2.145
145.85.2.146
145.85.2.147
145.85.2.148
145.85.2.154
145.85.2.161
145.85.2.162
145.85.2.167
145.85.2.168
145.85.2.169
145.85.2.171
145.85.2.172
145.85.2.174
145.85.2.175
145.85.2.177
145.85.2.189
145.85.2.190
145.85.2.192
145.85.2.195
145.85.2.197
145.85.2.198
145.85.2.199
145.85.2.203
145.85.2.204
145.85.2.207
145.85.2.211
145.85.2.213
145.85.2.217
145.85.2.223
145.85.2.228
145.85.2.229
145.85.2.230
145.85.2.233
145.85.2.234
145.85.2.236
145.85.2.238
145.85.2.239
145.85.2.244
145.85.2.248
145.85.2.254
145.85.9.104
145.85.9.110
145.85.139.5
145.85.139.8
145.85.139.9
185.136.64.6
185.136.64.7
185.136.65.6
185.136.65.7
213.227.143.160
2a00:4e40:1:1::2:204

[*] Emails found: 32
----------------------
ace-international@fontys.nl
ace@fontys.nl
campusvenlo@fontys.nl
deeltijdfhict@fontys.nl
e.vandervorst@student.fontys.nl
educatievedienstverlening@fontys.nl
fhict-academictransfer@fontys.nl
fhict-innovationlab@fontys.nl
fhkcircus@fontys.nl
fhmg-onderwijsenonderzoek@fontys.nl
fontyskaart@fontys.nl
info@fontys.nl
innovatiehub@fontys.nl
int.wirtschaft@fontys.nl
joep.peeters@fontys.nl
last@fontys.nl
m.devocht@fontys.nl
makeitwork@fontys.nl
mediatheek-eindhoven-dewittedame@fontys.nl
mjgm.vissers@fontys.nl
p.gorissen@fontys.nl
partnersict@fontys.nl
pcn@fontys.nl
pcn@student.fontys.nl
recruitment-fhict@fontys.nl
ssc-venlo@fontys.nl
studycommunication@fontys.nl
x22e.vandervorst@student.fontys.nl
x22innovatiehub@fontys.nl
x22joep.peeters@fontys.nl
x22makeitwork@fontys.nl
x22mediatheek-eindhoven-dewittedame@fontys.nl

[*] Hosts found: 1723
---------------------
0365.fontys.nl:o365.fontys.nl.
0365.fontys.nl:145.85.2.154
0365.fontys.nl:o365.fontys.nl
2525adfs2.fontys.nl
25adfs2.fontys.nl
365.fontys.nl:o365.fontys.nl
365.fontys.nl:o365.fontys.nl.
aallesoverict.fontys.nl
abs.fontys.nl
academic.lexisnexis.nl.lib.fontys.nl:145.85.2.138
academic.lexisnexis.nl.lib.fontys.nl:145.85.2.19
acapps.fontys.nl
acbireporting.fontys.nl
acconnect.fontys.nl
acjouw.fontys.nl:145.85.2.171
aclandanatomy.com.lib.fontys.nl:145.85.2.138
acmy.fontys.nl
acstudapp.fontys.nl
adfs.fontys.nl
adfs2.fontys.nl:145.85.2.15
advance-lexis-com.lib.fontys.nl:145.85.2.138
aff-mail.fontys.nl
aff.fontys.nl
ag.fontys.nl
agwaftest.fontys.nl:20.61.11.181
aiken.fontys.nl
alagon.fontys.nl:10.225.114.9
alameda.fontys.nl
alamosa.fontys.nl
allesoverict.fontys.nl:145.85.2.21
antwoordgroep.fontys.nl
anywhere365.fontys.nl
api.fontys.nl:145.85.2.119
app-proxy.fontys.nl
applicaties.fontys.nl:145.85.2.186
apps.democonnect.fontys.nl
apps.fontys.nl
apps.stagingconnect.fontys.nl
arsaequi.nl.lib.fontys.nl:145.85.2.138
artemis.fthv.fontys.nl:145.93.27.64
arwen.fthv.fontys.nl:145.93.27.14
as.im.fontys.nl
as.taim.fontys.nl
asa-vpn.fontys.nl:145.85.2.254
athena-hi.fontys.nl
athene.fthv.fontys.nl:145.93.27.44
atlas.fthv.fontys.nl:145.93.27.71
atlas.fthv.fontys.nl:145.93.27.70
atlas.fthv.fontys.nl:145.93.27.69
atlas.fthv.fontys.nl:145.93.27.68
autodiscover.fontys.nl:autodiscover.outlook.com
autodiscover.fontys.nl:autod.ha-autod.office.com
autodiscover.fontys.nl:40.99.204.8, 40.101.19.152, 40.99.205.56, 40.101.121.40
autodiscover.fontys.nl:autod.ms-acdc-autod.office.com
autodiscover.fontys.nl:autodiscover.outlook.com.
autodiscover.student.fontys.nl:autodiscover.outlook.com
autodiscover.student.fontys.nl:autod.ms-acdc-autod.office.com
autodiscover.student.fontys.nl:autodiscover.outlook.com.
autodiscover.student.fontys.nl:40.101.80.184, 40.99.205.56, 40.99.204.8, 52.97.201.104
autodiscover.student.fontys.nl:autod.ha-autod.office.com
automotiveplanner.fontys.nl
avlync.fontys.nl:145.85.2.59
avlync.fontys.nl:145.85.2.59, 145.85.2.149
avlync.fontys.nl:145.85.2.149
b3netapi.fontys.nl
banias.fontys.nl
bedrijven.hi.fontys.nl:intranet.hi.fontys.nl
bedrijven.hi.fontys.nl:intranet.hi.fontys.nl.
beheer.fontys.nl:145.85.2.138
beheer.fontys.nl:145.85.2.137
beheer.jobs.fontys.nl:5.206.215.46
beheer2.fontys.nl
beheer2.fontys.nl:145.85.2.138
bireporting.fontys.nl
bitlbee.il.fontys.nl:194.26.13.20
blade1.fthv.fontys.nl:145.93.27.132
blade2.fthv.fontys.nl:145.93.27.134
blade3.fthv.fontys.nl:145.93.27.136
blade4.fthv.fontys.nl:145.93.27.138
bouwkostenkompas.nl.lib.fontys.nl:145.85.2.138
branco.fontys.nl:145.85.224.11
brda-ilo.fontys.nl
brda.fontys.nl
bredbo.fontys.nl
broadcast.il.fontys.nl:194.26.13.63
broadcast.usernet.il.fontys.nl:194.26.13.127
bron.fontys.nl:52.18.143.49, 52.208.70.2, 54.77.247.215
bron.fontys.nl:ssl-bron-fontys-nl.presspage.com
bron.fontys.nl:ssl-bron-fontys-nl.presspage.com.
bw-a3-0-87.fthv.fontys.nl:145.93.27.236
bw-a4-0-81.fthv.fontys.nl:145.93.27.237
bw-a4-0-92.fthv.fontys.nl:145.93.27.238
bw-a4-0-97.fthv.fontys.nl:145.93.27.239
bw-a4-1-87.fthv.fontys.nl:145.93.27.240
bw-a4-1-87.fthv.fontys.nl:145.93.27.24
bw-a4-1-95.fthv.fontys.nl:145.93.27.241
c43656.fthv.fontys.nl:145.93.31.121
c43657.fthv.fontys.nl:145.93.31.86
c43673.fthv.fontys.nl:145.93.28.12
c43673.fthv.fontys.nl:145.93.28.120
c43674.fthv.fontys.nl:145.93.28.134
c43675.fthv.fontys.nl:145.93.28.104
c43676.fthv.fontys.nl:145.93.28.109
c43677.fthv.fontys.nl:145.93.28.106
c43678.fthv.fontys.nl:145.93.28.113
c43679.fthv.fontys.nl:145.93.28.119
c43680.fthv.fontys.nl:145.93.28.118
c43681.fthv.fontys.nl:145.93.31.156
c43682.fthv.fontys.nl:145.93.28.111
c43683.fthv.fontys.nl:145.93.28.129
c43684.fthv.fontys.nl:145.93.28.117
c43685.fthv.fontys.nl:145.93.28.102
c43686.fthv.fontys.nl:145.93.28.11
c43686.fthv.fontys.nl:145.93.28.110
c43687.fthv.fontys.nl:145.93.28.138
c43688.fthv.fontys.nl:145.93.31.135
c43689.fthv.fontys.nl:145.93.31.159
c43690.fthv.fontys.nl:145.93.31.160
c43690.fthv.fontys.nl:145.93.31.16
c43691.fthv.fontys.nl:145.93.31.150
c43691.fthv.fontys.nl:145.93.31.15
c43692.fthv.fontys.nl:145.93.31.152
c43693.fthv.fontys.nl:145.93.31.99
c43694.fthv.fontys.nl:145.93.31.92
c43695.fthv.fontys.nl:145.93.31.153
c43696.fthv.fontys.nl:145.93.31.143
c43697.fthv.fontys.nl:145.93.31.139
c43698.fthv.fontys.nl:145.93.31.161
c43699.fthv.fontys.nl:145.93.31.149
c43700.fthv.fontys.nl:145.93.31.151
c43701.fthv.fontys.nl:145.93.31.144
c43702.fthv.fontys.nl:145.93.31.94
c43703.fthv.fontys.nl:145.93.31.107
c43704.fthv.fontys.nl:145.93.31.190
c43704.fthv.fontys.nl:145.93.31.19
c43705.fthv.fontys.nl:145.93.31.197
c43706.fthv.fontys.nl:145.93.31.108
c43707.fthv.fontys.nl:145.93.31.73
c43708.fthv.fontys.nl:145.93.31.196
c43709.fthv.fontys.nl:145.93.31.206
c43710.fthv.fontys.nl:145.93.31.84
c43711.fthv.fontys.nl:145.93.31.75
c43712.fthv.fontys.nl:145.93.28.139
c43713.fthv.fontys.nl:145.93.31.173
c43714.fthv.fontys.nl:145.93.31.82
c43715.fthv.fontys.nl:145.93.31.122
c43716.fthv.fontys.nl:145.93.31.113
c43717.fthv.fontys.nl:145.93.31.112
c43718.fthv.fontys.nl:145.93.31.131
c43719.fthv.fontys.nl:145.93.31.114
c43720.fthv.fontys.nl:145.93.31.192
c43721.fthv.fontys.nl:145.93.31.138
c43722.fthv.fontys.nl:145.93.31.88
c43723.fthv.fontys.nl:145.93.31.182
c43724.fthv.fontys.nl:145.93.31.181
c43725.fthv.fontys.nl:145.93.31.130
c43725.fthv.fontys.nl:145.93.31.13
c43726.fthv.fontys.nl:145.93.31.175
c43727.fthv.fontys.nl:145.93.31.101
c43728.fthv.fontys.nl:145.93.31.133
c43729.fthv.fontys.nl:145.93.31.83
c43730.fthv.fontys.nl:145.93.31.81
c43731.fthv.fontys.nl:145.93.31.110
c43731.fthv.fontys.nl:145.93.31.11
c43732.fthv.fontys.nl:145.93.31.132
c43733.fthv.fontys.nl:145.93.31.4
c43734.fthv.fontys.nl:145.93.31.127
c43735.fthv.fontys.nl:145.93.31.155
c43736.fthv.fontys.nl:145.93.31.158
c43737.fthv.fontys.nl:145.93.31.198
c43738.fthv.fontys.nl:145.93.31.71
c43739.fthv.fontys.nl:145.93.31.136
c43740.fthv.fontys.nl:145.93.31.200
c43740.fthv.fontys.nl:145.93.28.136
c43741.fthv.fontys.nl:145.93.31.163
c43742.fthv.fontys.nl:145.93.31.141
c43743.fthv.fontys.nl:145.93.31.146
c43745.fthv.fontys.nl:145.93.31.154
c43746.fthv.fontys.nl:145.93.31.142
c43747.fthv.fontys.nl:145.93.31.80
c43747.fthv.fontys.nl:145.93.31.8
c43748.fthv.fontys.nl:145.93.31.116
c43749.fthv.fontys.nl:145.93.31.9
c43749.fthv.fontys.nl:145.93.31.90
c43750.fthv.fontys.nl:145.93.31.74
c43751.fthv.fontys.nl:145.93.31.105
c43752.fthv.fontys.nl:145.93.31.91
c43753.fthv.fontys.nl:145.93.31.147
c43754.fthv.fontys.nl:145.93.31.199
c43755.fthv.fontys.nl:145.93.31.169
c43757.fthv.fontys.nl:145.93.31.171
c43758.fthv.fontys.nl:145.93.31.194
c43759.fthv.fontys.nl:145.93.28.127
c43760.fthv.fontys.nl:145.93.31.97
c43761.fthv.fontys.nl:145.93.28.107
c43762.fthv.fontys.nl:145.93.28.133
c43763.fthv.fontys.nl:145.93.31.170
c43763.fthv.fontys.nl:145.93.31.17
c43764.fthv.fontys.nl:145.93.31.172
c43765.fthv.fontys.nl:145.93.31.178
c43766.fthv.fontys.nl:145.93.31.95
c43768.fthv.fontys.nl:145.93.28.14
c43768.fthv.fontys.nl:145.93.28.140
c43769.fthv.fontys.nl:145.93.31.93
c43770.fthv.fontys.nl:145.93.31.103
c43771.fthv.fontys.nl:145.93.31.176
c43772.fthv.fontys.nl:145.93.31.12
c43772.fthv.fontys.nl:145.93.31.120
c43773.fthv.fontys.nl:145.93.31.204
c43774.fthv.fontys.nl:145.93.31.203
c43775.fthv.fontys.nl:145.93.31.96
c43776.fthv.fontys.nl:145.93.31.14
c43776.fthv.fontys.nl:145.93.31.140
c43777.fthv.fontys.nl:145.93.31.205
c43778.fthv.fontys.nl:145.93.31.1
c43778.fthv.fontys.nl:145.93.31.100
c43779.fthv.fontys.nl:145.93.28.122
c43780.fthv.fontys.nl:145.93.28.121
c43781.fthv.fontys.nl:145.93.31.128
c43782.fthv.fontys.nl:145.93.31.134
c43783.fthv.fontys.nl:145.93.31.111
c43784.fthv.fontys.nl:145.93.28.126
c43785.fthv.fontys.nl:145.93.31.157
c43786.fthv.fontys.nl:145.93.31.79
c43787.fthv.fontys.nl:145.93.28.103
c43788.fthv.fontys.nl:145.93.28.114
c43789.fthv.fontys.nl:145.93.28.137
c43790.fthv.fontys.nl:145.93.28.116
c43791.fthv.fontys.nl:145.93.28.1
c43791.fthv.fontys.nl:145.93.28.100
c43792.fthv.fontys.nl:145.93.28.123
c43793.fthv.fontys.nl:145.93.28.125
c43794.fthv.fontys.nl:145.93.28.112
c43795.fthv.fontys.nl:145.93.28.115
c43796.fthv.fontys.nl:145.93.28.124
c43797.fthv.fontys.nl:145.93.28.108
c43798.fthv.fontys.nl:145.93.28.135
c43799.fthv.fontys.nl:145.93.28.101
c43800.fthv.fontys.nl:145.93.28.132
c43801.fthv.fontys.nl:145.93.31.148
c43802.fthv.fontys.nl:145.93.31.165
c43806.fthv.fontys.nl:145.93.31.118
c43807.fthv.fontys.nl:145.93.31.202
c43808.fthv.fontys.nl:145.93.28.131
c43810.fthv.fontys.nl:145.93.31.164
c43811.fthv.fontys.nl:145.93.31.115
c43813.fthv.fontys.nl:145.93.31.119
c43814.fthv.fontys.nl:145.93.31.145
c43815.fthv.fontys.nl:145.93.31.78
c43816.fthv.fontys.nl:145.93.31.195
c43817.fthv.fontys.nl:145.93.31.166
c43818.fthv.fontys.nl:145.93.31.89
c43819.fthv.fontys.nl:145.93.31.179
c43820.fthv.fontys.nl:145.93.31.184
c43821.fthv.fontys.nl:145.93.31.168
c43822.fthv.fontys.nl:145.93.31.109
c43823.fthv.fontys.nl:145.93.31.174
c43824.fthv.fontys.nl:145.93.31.123
c43825.fthv.fontys.nl:145.93.31.191
c43826.fthv.fontys.nl:145.93.31.185
c43827.fthv.fontys.nl:145.93.31.104
c43828.fthv.fontys.nl:145.93.31.129
c43829.fthv.fontys.nl:145.93.31.162
c43830.fthv.fontys.nl:145.93.31.77
c43831.fthv.fontys.nl:145.93.31.76
c43832.fthv.fontys.nl:145.93.31.124
c43833.fthv.fontys.nl:145.93.31.102
c43834.fthv.fontys.nl:145.93.31.186
c43835.fthv.fontys.nl:145.93.31.18
c43835.fthv.fontys.nl:145.93.31.180
c43836.fthv.fontys.nl:145.93.31.183
c43837.fthv.fontys.nl:145.93.31.87
c43838.fthv.fontys.nl:145.93.31.193
c43839.fthv.fontys.nl:145.93.31.106
c43840.fthv.fontys.nl:145.93.28.15
c43840.fthv.fontys.nl:145.93.28.150
c43841.fthv.fontys.nl:145.93.31.167
c43842.fthv.fontys.nl:145.93.28.128
c43843.fthv.fontys.nl:145.93.28.130
c43843.fthv.fontys.nl:145.93.28.13
c43844.fthv.fontys.nl:145.93.31.188
c43845.fthv.fontys.nl:145.93.31.117
c43846.fthv.fontys.nl:145.93.31.189
c43847.fthv.fontys.nl:145.93.31.126
c43848.fthv.fontys.nl:145.93.31.85
c43849.fthv.fontys.nl:145.93.31.187
c43850.fthv.fontys.nl:145.93.28.105
cag.fontys.nl:145.85.2.30
cagayan.fontys.nl:145.85.7.25
canning.fontys.nl:145.85.35.101
canoochee.fontys.nl:145.85.35.103
canvas.fontys.nl:52.48.141.201, 52.48.116.163, 54.171.52.164
canvas.fontys.nl:canvas-vanity-fontys-115898053.eu-west-1.elb.amazonaws.com
canvas.fontys.nl:fontys-vanity.instructure.com
canvas.fontys.nl:fontys-vanity.instructure.com.
canvas.fontys.nl:54.171.52.164, 52.48.116.163, 52.48.141.201
cape.fontys.nl:145.85.2.15
charm.il.fontys.nl:194.26.13.34
citrixdesktopdirector.fontys.nl
companydashboard-lexisnexis-nl.lib.fontys.nl:145.85.2.138
connect.fontys.nl:145.85.2.168
copper.fontys.nl:145.85.2.220
crl.fontys.nl:145.85.2.56
crm.fontys.nl:145.85.2.24
crmnext.fontys.nl:145.85.2.27
crmnext2.fontys.nl
csg.fontys.nl
ctm.fontys.nl
da.fontys.nl:145.85.2.148
democonnect.fontys.nl
democonnect.fontys.nl:145.85.2.153
devapp.fontys.nl:20.61.11.181
devcon1.fontys.nl
devcon2.fontys.nl
devcon3.fontys.nl
devjouw-api.fontys.nl:20.61.11.181
devjouw.fontys.nl:20.61.11.181
dialin.fontys.nl:145.85.2.136
directaccess.fontys.nl:145.85.2.101
discoverreceiver.fontys.nl
discoverreceiver.student.fontys.nl
dna.fontys.nl
dnscache0.il.fontys.nl:194.26.13.5
dnscache1.il.fontys.nl:194.26.13.6
download.im.fontys.nl
download.springer.com.lib.fontys.nl:145.85.2.138
download.taim.fontys.nl
dpf-hi.fontys.nl:145.85.7.33
dpkgklaes-hi.fontys.nl:145.85.4.11
drau.fontys.nl:145.85.2.12
duero-ilo.fontys.nl
dummy.studyabroad.fontys.nl:145.85.2.123
dvjouw.fontys.nl:145.85.2.121
dvjouw.fontys.nl:13.80.70.51
echo360.fontys.nl:145.85.7.51
edge1.fthv.fontys.nl:145.93.27.84
edge2.fthv.fontys.nl:145.93.27.80
edge2.fthv.fontys.nl:145.93.27.8
ehv-srvhost-rmd.fontys.nl:194.171.92.20
einstein.fthv.fontys.nl:145.93.27.45
elo.fontys.nl:145.85.2.16
elo2.fontys.nl:145.85.2.17
elo3.fontys.nl
elo4.fontys.nl:145.85.2.167
elo4.fontys.nl
elospbs.fontys.nl:145.85.7.77
elotest.fontys.nl
enterpriseregistration.fontys.nl:145.85.2.15
enterpriseregistration.relatie.fontys.nl
enterpriseregistration.student.fontys.nl:145.85.2.15
eowyn.fthv.fontys.nl:145.93.27.12
eragon.fthv.fontys.nl:145.93.27.81
erebos.fthv.fontys.nl:145.93.27.2
eric.fontys.nl
eric2.fontys.nl
eric2.fontys.nl.eric3.fontys.nl
eric3.fontys.nl
eric4.fontys.nl
eric5.fontys.nl
esx1.fthv.fontys.nl:145.93.27.130
esx1.fthv.fontys.nl:145.93.27.13
etymologie.nl.lib.fontys.nl:145.85.2.138
eumportal.fontys.nl
euromonitor.com.lib.fontys.nl:145.85.2.138
f5nlb11.fontys.nl
f5nlb51.fontys.nl
fbs.fontys.nl
fea.fontys.nl:145.85.2.138
fhict-extern.fontys.nl:145.85.7.18
fhict.fontys.nl:145.85.4.5
fhj.fontys.nl
fils.fontys.nl:145.85.7.24
fisher.fontys.nl:145.85.2.6
fontyspresenter.fontys.nl:145.85.2.26
fs9a.fontys.nl
fs9dm.fontys.nl
fs9o.fontys.nl
fs9p.fontys.nl
fs9t.fontys.nl
fuerte-ilo.fontys.nl
fysiovaardig.boom.nl.lib.fontys.nl:145.85.2.138
gaia.fthv.fontys.nl:145.93.27.53
galadriel.fthv.fontys.nl:145.93.27.65
goto.fontys.nl:145.85.2.118
gradework.fontys.nl
grandcru.il.fontys.nl:194.26.13.47
grouphub.fontys.nl
guadiana.fontys.nl
gve.fontys.nl
gx.fontys.nl:145.85.2.109
hebe.fthv.fontys.nl:145.93.27.51
helena.fthv.fontys.nl:145.93.27.82
helios.fthv.fontys.nl:145.93.27.151
heracles.fontys.nl:145.85.2.3
herman.fontys.nl
hermes.fontys.nl:145.85.2.2
hi.fontys.nl:fshio01.hi.fontys.nl
hi.fontys.nl:fshio01.hi.fontys.nl.
hoegaarden.il.fontys.nl:194.26.13.40
hp_color_laserjet3700_194.fthv.fontys.nl:145.93.28.4
hse-sdu-nl.lib.fontys.nl:145.85.2.138
hub.fontys.nl:18.192.85.207
hurling-frootmig.il.fontys.nl:194.26.13.33
hyde.il.fontys.nl:194.26.13.48
hyperion.fthv.fontys.nl:145.93.27.128
i453.fontys.nl:18.154.22.49, 18.154.22.11, 18.154.22.83, 18.154.22.37
i453.fontys.nl:108.139.1.61
i453.fontys.nl:13.226.153.82, 13.226.153.37, 13.226.153.66, 13.226.153.32
ibis.fthv.fontys.nl:145.93.27.66
ideal.fontys.nl:145.85.2.64
identity.fontys.nl:145.85.2.65
identity.fontys.nl
ijssel.fontys.nl:145.85.35.28
ilbd.il.fontys.nl:194.26.13.15
ilnet.il.fontys.nl:194.26.13.0
im.fontys.nl
include.fontys.nl
infoconnect.fontys.nl:145.85.2.34
infoconnect2.fontys.nl:145.85.2.34
inlog.jobs.fontys.nl:213.227.143.160
intelligence.communicatieonline.nl.lib.fontys.nl:145.85.2.138
intelligence.marketingonline.nl.lib.fontys.nl:145.85.2.138
intern.fontys.nl:145.85.2.239
intern2.fontys.nl
intranet.hi.fontys.nl:145.85.7.58
iplanner.fontys.nl:145.85.2.129
iplanner.fontys.nl
ipmonitor.fontys.nl
irc.il.fontys.nl:194.26.13.9
itreports.fontys.nl:145.85.2.29
itsm.fontys.nl:145.85.2.32
itsma.fontys.nl
itsminfo.fontys.nl:145.85.2.238
itsmsurvey.fontys.nl
itsmt.fontys.nl
itsmtools.fontys.nl:145.85.2.33
ittfs.fontys.nl
iwebfiles.fontys.nl
jobs.fontys.nl:5.206.215.46
jobs.fontys.nl:jobs-fontys-nl.mail.protection.outlook.com.
jobs.fontys.nl:jobs-fontys-nl.mail.protection.outlook.com
jouw.fontys.nl:145.85.2.37
jukebox.il.fontys.nl:194.26.13.13
katatonic.il.fontys.nl:194.26.13.73
kbs.fontys.nl:145.85.2.94
keuzegids.org.lib.fontys.nl:145.85.2.138
keuzegids.org.lib.fontys.nl:145.85.2.19
kha.nl.lib.fontys.nl:145.85.2.138
kha.nl.lib.fontys.nl:145.85.2.19
kharon.fthv.fontys.nl:145.93.27.3
knox.fontys.nl
kong.fontys.nl
ldaps.fontys.nl
legacy.fontys.nl
lexisnexis.nl.lib.fontys.nl:145.85.2.138
lexisnexis.nl.lib.fontys.nl:145.85.2.19
lib.fontys.nl:145.85.2.138
lib.fontys.nl:145.85.2.19
lib2.fontys.nl:145.85.2.19
lib2.fontys.nl
library.fontys.nl
library.fontys.nl:145.85.2.94
lic-3252-01.fontys.nl:ijssel.fontys.nl.
lic-3252-01.fontys.nl:ijssel.fontys.nl
lic-3393-01.fontys.nl:ijssel.fontys.nl.
lic-3393-01.fontys.nl:ijssel.fontys.nl
lic-3561-01.fontys.nl:ijssel.fontys.nl
lic-3561-01.fontys.nl:ijssel.fontys.nl.
lic-fred-01.fontys.nl:alagon.fontys.nl.
lic-fred-01.fontys.nl:alagon.fontys.nl
licy.fthv.fontys.nl:145.93.27.101
link-springer-com.lib.fontys.nl:145.85.2.138
link.springer.com.lib.fontys.nl:145.85.2.19
link.springer.com.lib.fontys.nl:145.85.2.138
lists.il.fontys.nl:194.26.13.14
locker.fontys.nl
login.fontys.nl
login.lib.fontys.nl:145.85.2.138
lopabo.fontys.nl:145.85.61.148
luthien.fthv.fontys.nl:145.93.27.17
lync.fontys.nl
lyncdiscover.fontys.nl:145.85.2.136
lyncdiscover.student.fontys.nl:145.85.2.136
m.fontys.nl:145.85.2.47
m365.fontys.nl:o365.fontys.nl.
m365.fontys.nl:145.85.2.154
m365.fontys.nl:o365.fontys.nl
maat.fthv.fontys.nl:145.93.27.102
mail.fontys.nl:145.85.2.138
mail.il.fontys.nl:194.26.13.7
mail2.fontys.nl:145.85.2.206
malina.fthv.fontys.nl:145.93.27.150
malina.fthv.fontys.nl:145.93.27.15
marcel.fontys.nl
marvin.il.fontys.nl:194.26.13.36
mbrtpacs.fontys.nl:145.85.2.49
mbrtpacs02.fontys.nl
mediasite.fontys.nl
medusa.il.fontys.nl:194.26.13.37
meet.fontys.nl:145.85.2.136
meet.student.fontys.nl:145.85.2.136
mfa.fontys.nl:145.85.2.134
mfcm-dev.fontys.nl:13.80.70.51
mfcm-dev.fontys.nl:145.85.2.146
mfcm.fontys.nl:145.85.2.140
microsoft.fontys.nl:o365.fontys.nl
microsoft.fontys.nl:o365.fontys.nl.
microsoft.fontys.nl:145.85.2.154
microsoft365.fontys.nl:145.85.2.154
microsoft365.fontys.nl:o365.fontys.nl.
microsoft365.fontys.nl:o365.fontys.nl
mississippi.fontys.nl
mmp.fontys.nl
mobile.fontys.nl:145.85.2.47
monolith.il.fontys.nl:194.26.13.39
moodle.fontys.nl
mr-aci-p3.fontys.nl
mr-dienstit-s1.fontys.nl
mr-er-476.fontys.nl
mr-er-m.fontys.nl
mr-es-m.fontys.nl
mr-fhbent-r1.fontys.nl
mr-fhmg-tf.fontys.nl
mr-fhss-tf-2112.fontys.nl
mr-fhss-tf-2113.fontys.nl
mr-flot-p1.fontys.nl
mr-fph-tf-0103.fontys.nl
mr-fph-tf-0104.fontys.nl
mr-fsh-ek.fontys.nl
mr-hrmp-es.fontys.nl
mr-p1-f204.fontys.nl
mr-ped-cl.fontys.nl
mr-ped-s3.fontys.nl
mr-r3-270.fontys.nl
mr-r3-m.fontys.nl
msdnld-hi.fontys.nl:145.85.4.2
mse.fontys.nl:145.85.2.82
mx1.il.fontys.nl:194.26.13.8
my.democonnect.fontys.nl
my.democonnect.fontys.nl:145.85.2.153
my.fontys.nl:145.85.2.168
my.fontys.nl:145.85.2.168tasprt-01.fontys.nl:145.85.30.217
my.sprme.fontys.nl
my.stagingconnect.fontys.nl
my.stagingconnect.fontys.nl:145.85.2.177
mysite.fontys.nl
narew.fontys.nl:145.85.2.74
netpointpth.fontys.nl:194.171.92.21
netscaler01.fontys.nl
newton.fthv.fontys.nl:145.93.27.46
nl.lib.fontys.nl:145.85.2.19
nls.fontys.nl
ns1.il.fontys.nl:194.26.13.4
nymboida.fontys.nl:145.85.2.7
o365.fontys.nl:145.85.2.154
ocs.fontys.nl
office.fontys.nl:o365.fontys.nl.
office.fontys.nl:o365.fontys.nl
office.fontys.nl:145.85.2.154
office365.fontys.nl:o365.fontys.nl.
office365.fontys.nl:145.85.2.154
office365.fontys.nl:o365.fontys.nl
omnisoap.fontys.nl:145.85.2.234
omnisoap2.fontys.nl
online-goinglobal-com.lib.fontys.nl:145.85.2.138
onlinelibrary-wiley-com.lib.fontys.nl:145.85.2.138
onlinelibrary-wileycom.lib.fontys.nl:145.85.2.138
opensimpth.fontys.nl:194.171.92.27
orange.fontys.nl:194.171.92.22
oso.fontys.nl:145.85.2.88
osolms.fontys.nl:145.85.2.88
outlook.fontys.nl:145.85.2.112
ovoc.fontys.nl
ow4.fontys.nl
owbireporting.fontys.nl
owcrm.fontys.nl
owcrmnext.fontys.nl:40.112.89.123
owcrmnext.fontys.nl:145.85.2.192
owcrmnext.fontys.nl:13.80.70.51
owexchange.fontys.nl:145.85.31.47
owgoto.fontys.nl:145.85.2.141
owintern.fontys.nl
owjouw.fontys.nl:145.85.2.145
owstudapp.fontys.nl
owwebservice.fontys.nl
p8verlicht.fontys.nl
p8verlicht1.fontys.nl:145.85.139.5
p8verlicht2.fontys.nl:145.85.139.6
p8verlicht3.fontys.nl:145.85.139.7
p8verlicht4.fontys.nl:145.85.139.8
p8verlicht5.fontys.nl:145.85.139.9
pabotil.fontys.nl
parabel.fontys.nl
parkbase.fontys.nl
pasfoto.fontys.nl:145.85.2.138
pechora.fontys.nl:145.85.2.215
peedee.fontys.nl:145.85.37.125
pegasus.fontys.nl:145.85.2.6, 145.85.2.7
pegasus.fontys.nl:145.85.2.6
pegasus.fontys.nl:145.85.2.7
penguin.il.fontys.nl:194.26.13.35
picarta.nl.lib.fontys.nl:145.85.2.138
picarta.pica.nl.lib.fontys.nl:145.85.2.138
pico1.e.ft.fontys.nl:145.85.4.128
pinega.fontys.nl
pocag.fontys.nl
pocda.fontys.nl
ponoy.fontys.nl
ponsul.fontys.nl
poonch.fontys.nl
poplar.fontys.nl
popple.fontys.nl
porce.fontys.nl
porijogi.fontys.nl
portal.fontys.nl:145.85.2.138
portal2.fontys.nl
pri-router.ilnet.il.fontys.nl:194.26.13.2
pri-router.usernet.il.fontys.nl:194.26.13.66
print.fontys.nl:145.85.38.40
priva.fontys.nl:145.85.2.52
ps-helpdesk.fontys.nl
ps-personeel.fontys.nl
ps-portal.fontys.nl
ps-student.fontys.nl
pv.perfectview.fontys.nl:185.136.64.6, 185.136.64.7, 185.136.65.6, 185.136.65.7
qmanage.fontys.nl:145.85.35.40
quweiq.fontys.nl
r1-398-mon1.fontys.nl:145.85.51.49
r1-398-mon2.fontys.nl:145.85.51.50
r1-398-mon3.fontys.nl:145.85.51.51
r1-398-mon4.fontys.nl:145.85.51.52
r1-398-proj.fontys.nl:145.85.51.53
r5-022-av.gve.fontys.nl
ra.fontys.nl:145.85.2.147
ra.fontys.nl
ra.fthv.fontys.nl:145.93.27.153
raba.fontys.nl:145.85.2.13
radius.fontys.nl
re.fontys.nl
recordingbox.fontys.nl:145.85.4.39
redactie.fontys.nl:145.85.2.167
redactiegx.fontys.nl:145.85.2.167
redirect.fontys.nl
reserveringen-preprod.fontys.nl:145.85.2.172
reserveringen-staging.fontys.nl
reserveringen.fontys.nl:145.85.2.172
rgs.fontys.nl
rhea.fthv.fontys.nl:145.93.27.4
rhea.fthv.fontys.nl:145.93.27.5
rm.fontys.nl
rme.fontys.nl
rmow.fontys.nl
rmow.fontys.nl:145.85.2.198
rmsp.fontys.nl
rmspe.fontys.nl
robofontys-hi.fontys.nl:145.85.4.30
rooster.fontys.nl:145.85.2.199
rooster.fontys.nl
roostertest.fontys.nl
roostertest.fontys.nl:145.85.2.201
router.ilnet.il.fontys.nl:194.26.13.1
router.usernet.il.fontys.nl:194.26.13.65
rpcmail.fontys.nl
rvbblog.fontys.nl
s24820.fthv.fontys.nl:145.93.31.5
samenwebben.fontys.nl
samenwebben.fontys.nl:145.85.2.203
samenwebbenrd.fontys.nl:145.85.2.204
samenwebbenrd.fontys.nl
sar.fontys.nl
sbc1.fontys.nl:145.85.2.126
sbc2.fontys.nl:145.85.2.127
scominfo.fontys.nl
search.proquest.com.lib.fontys.nl:145.85.2.138
sebiweb.fontys.nl:145.93.27.10
sec-router.ilnet.il.fontys.nl:194.26.13.3
sec-router.usernet.il.fontys.nl:194.26.13.67
secapi.fontys.nl:145.85.2.174
secapi2.fontys.nl:145.85.2.174
secure.fontys.nl
seman.fontys.nl
servicehighway.fontys.nl
shoarma.il.fontys.nl:194.26.13.74
signin.fontys.nl:145.85.2.46
sil.fontys.nl
sip.fontys.nl:145.85.2.44, 145.85.2.102
sip.fontys.nl:145.85.2.44
sip.fontys.nl:145.85.2.102
sip.student.fontys.nl:145.85.2.44, 145.85.2.102
sip.student.fontys.nl:145.85.2.44
sip.student.fontys.nl:145.85.2.102
sitebouwer.fontys.nl
sl2.fontys.nl:145.85.23.169
slc.fontys.nl:145.85.23.169
slp.fontys.nl:145.85.23.71
smtp.fontys.nl:40.74.22.195
smtp1.fontys.nl:smtp.fontys.nl.
smtp1.fontys.nl:smtp.fontys.nl
smtp1.fontys.nl:40.74.22.195
smtp2.fontys.nl:smtp.fontys.nl
smtp2.fontys.nl:40.74.22.195
softgrid.fthv.fontys.nl:145.93.27.96
softgrid.fthv.fontys.nl:145.93.27.95
softgrid2.fthv.fontys.nl:145.93.27.97
softgrid3.fthv.fontys.nl:145.93.27.98
software.fontys.nl
spijkerboor.fontys.nl
springer.com.lib.fontys.nl:145.85.2.19
springer.com.lib.fontys.nl:145.85.2.138
sprme-apps.fontys.nl
sprme.fontys.nl
sql2.fthv.fontys.nl:145.93.27.99
ssosecapi.fontys.nl:145.85.2.175
st2crmnext.fontys.nl
staging.fontys.nl
stagingconnect.fontys.nl:145.85.2.177
stagingconnect.fontys.nl
stagingrd.fontys.nl
stagingredactie.fontys.nl
stagingredactierd.fontys.nl
stagingredactiewm10.fontys.nl
stagingwm10.fontys.nl
stapi.fontys.nl:145.85.2.189
stbireporting.fontys.nl
stcrm.fontys.nl:13.80.70.51
stcrm.fontys.nl:40.112.89.123
stcrm.fontys.nl:145.85.2.190
stcrmnext.fontys.nl:13.80.70.51
stcrmnext.fontys.nl:145.85.2.192
stgoto.fontys.nl:145.85.2.207
stgoto.fontys.nl:40.112.89.123
stgoto.fontys.nl:13.80.70.51
stidentity.fontys.nl
stidentity.fontys.nl:145.85.2.213
stintern.fontys.nl:145.85.2.217
stintern.fontys.nl:13.80.70.51
stintern.fontys.nl:40.112.89.123
stjouw.fontys.nl:40.112.89.123
stjouw.fontys.nl:13.80.70.51
stjouw.fontys.nl:145.85.2.223
stjouwinfo.fontys.nl:145.85.2.233
storage.fontys.nl:145.85.2.176
stsecapi.fontys.nl:145.85.2.53
stssosecapi.fontys.nl
stucomm-api-acc.fontys.nl:145.85.2.229
stucomm-api-tst.fontys.nl:145.85.2.228
stucomm-api.fontys.nl:145.85.2.131
studapp.fontys.nl
student.fontys.nl:student-fontys-nl.mail.protection.outlook.com
student.fontys.nl:student-fontys-nl.mail.protection.outlook.com.
student.fontys.nl
studiekeuzecheck.fontys.nl
studielink2.fontys.nl:145.85.23.159
stwebservice.fontys.nl:145.85.2.195
stwebservices.fontys.nl
stwww.fontys.nl:145.85.2.28
sukke.il.fontys.nl:194.26.13.45
surya.fthv.fontys.nl:145.93.27.152
svnklaes-hi.fontys.nl:145.85.4.3
swalm.fontys.nl
syslog.fontys.nl
ta.fontys.nl
taabs.fontys.nl
taadfs.fontys.nl
taadfs2.fontys.nl:145.85.9.104
tabeheer.fontys.nl
tacrm.fontys.nl:145.85.2.248
tacrmnext.fontys.nl
tacsg.fontys.nl
tactm.fontys.nl
tada.fontys.nl
taelo.fontys.nl
taelo2.fontys.nl
taexchange.fontys.nl:145.85.30.188
tagingconnect.fontys.nl
taideal.fontys.nl
taim.fontys.nl:145.85.9.23
taim.fontys.nl
taiplanner.fontys.nl
tajouw.fontys.nl
tallesoverict.fontys.nl
tamail.fontys.nl:145.85.9.65
tamysite.fontys.nl:145.85.9.25
taocs.fontys.nl
tapegasus.fontys.nl:145.85.2.123
tapegasus.fontys.nl:145.85.2.122
taportal.fontys.nl:145.85.9.20
taprint.fontys.nl:145.85.30.217
taredactie.fontys.nl
tarpcmail.fontys.nl
tasecapi.fontys.nl:145.85.9.64
tasecure.fontys.nl
tasexedge-03.fontys.nl:145.85.2.68
tasexedge-04.fontys.nl:145.85.2.69
tasexhub-02.fontys.nl:145.85.30.184
tasprt-01.fontys.nl:145.85.30.217
tasprt-02.fontys.nl:145.85.30.39
tatest.fontys.nl
tawebconf.fontys.nl
tawebfiles.fontys.nl:145.85.9.28
tawebmail.fontys.nl
tawebservice.fontys.nl
tawerkplek.fontys.nl
tawww.fontys.nl:145.85.9.14
tawww3.fontys.nl
testwinssh.fthv.fontys.nl:145.93.27.54
tfs.fontys.nl
tfst.fontys.nl
timetellapp.fontys.nl:145.85.2.26
timetellweb.fontys.nl:145.85.2.83
timetellwebtest.fontys.nl:145.85.2.58
tmg.fontys.nl
tmgtest.fontys.nl
town-ilo.fontys.nl
town.fontys.nl
trim.fontys.nl
ucc.fontys.nl
uccreports.fontys.nl
uk-sagepub-com.lib.fontys.nl:145.85.2.138
underwood2.fthv.fontys.nl:145.93.27.67
usernet.il.fontys.nl:194.26.13.64
vd.fontys.nl
vdi.fontys.nl
vdtest.fontys.nl
vidris.fontys.nl
virtualapps-publish.fontys.nl
virtualapps.fontys.nl
voorlichting.fontys.nl:145.85.2.138
web-b-ebscohost-com.lib.fontys.nl:145.85.2.138
webapp.fontys.nl:145.85.2.135
webapp2.fontys.nl:145.85.2.162
webcon.fontys.nl:145.85.2.148
webcon.fontys.nl:145.85.2.45, 145.85.2.96, 145.85.2.148
webcon.fontys.nl:145.85.2.96
webcon.fontys.nl:145.85.2.45
webcon.student.fontys.nl:145.85.2.148
webcon.student.fontys.nl:145.85.2.45, 145.85.2.148
webcon.student.fontys.nl:145.85.2.45
webconf.fontys.nl
webdb.hi.fontys.nl:145.85.4.29
weber.il.fontys.nl:194.26.13.71
webext.fontys.nl:145.85.2.136
webext.student.fontys.nl:145.85.2.136
webfiles.fontys.nl:145.85.2.176
webmail.fontys.nl:145.85.2.138
webmail.il.fontys.nl:194.26.13.11
webmail2.fontys.nl
webservice.fontys.nl:145.85.2.196
webservice2.fontys.nl:145.85.2.196
webservices.fontys.nl
werkplek.fontys.nl:145.85.39.90
werkwijzer.fontys.nl:145.85.2.197
werkwijzers.fontys.nl:145.85.2.197
wifi.fontys.nl:145.85.2.138
wiki.il.fontys.nl:194.26.13.12
wordpress.fontys.nl
wsb3netapi.fontys.nl
wsgradework.fontys.nl
wsprogress.fontys.nl
wsxedule.fontys.nl
wsxedule.fontys.nl:145.85.2.170
wurm.fontys.nl:145.85.35.32
wvdstarter.fontys.nl:137.117.211.244
www-alurvs-nl.lib.fontys.nl:145.85.2.138
www-cas-org.lib.fontys.nl:145.85.2.138
www-coachlinkhogeronderwijs-nl.lib.fontys.nl:145.85.2.138
www-dev.il.fontys.nl:194.26.13.16
www-imaios-com.lib.fontys.nl:145.85.2.138
www-lexisnexis-com.lib.fontys.nl:145.85.2.138
www-nritmedia-nl.lib.fontys.nl:145.85.2.138
www-ntvg-nl.lib.fontys.nl:145.85.2.138
www-ntvg-nl.lib.fontys.nl:145.85.2.19
www-portal-euromonitor-com.lib.fontys.nl:145.85.2.138
www-sciencedirect-com.lib.fontys.nl:145.85.2.138
www-sdu-nl.lib.fontys.nl:145.85.2.138
www-statista-com.lib.fontys.nl:145.85.2.138
www-vilanskickprotocollen-nl.lib.fontys.nl:145.85.2.138
www-wiley-com.lib.fontys.nl:145.85.2.138
www-wiso-net-de.lib.fontys.nl:145.85.2.138
www-yindo-nl.lib.fontys.nl:145.85.2.138
www.fontys.nl:145.85.2.54
www.fontys.nl:145.85.2.119
www.ideal.fontys.nl
www.il.fontys.nl:194.26.13.10
www.p8verlicht1.fontys.nl
x22connect.fontys.nl
x22www.fontys.nl
xedule.fontys.nl
zaphod.il.fontys.nl:194.26.13.46
zeus.il.fontys.nl:194.26.13.70
zuidgat.fontys.nl
```

<br />