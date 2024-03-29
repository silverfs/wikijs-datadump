---
title: Web Security Attack and Defence
description: 
published: true
date: 2023-01-10T16:17:17.560Z
tags: 
editor: markdown
dateCreated: 2022-09-08T10:41:34.312Z
---



# Path traversal, File Inclusion and Command Injection
> The examples down below are made using Web-DVWA.
{.is-info}

<br />
<br />

**Path Traversal**
In order to understand path traversal, you'll have to have basic understanding of the linux filesystem and other known services like Apache. We'll learn more about that along the way.
Path traversal is a web vulnerability which makes use of the hosted application to view arbitrary files. These files could be from the application or from the system itself. This makes it possible to not only view, but potentially alter files to take full control over the system.

DVWA has a seperate subject called File Intrusion. Using this function, I tried some different methods for path traversal. 

In the example below, we can deduct a few things from looking at the url. Firstly, using the parameter `page=` which originally takes a specified file (file1.php), it will now take a new entry, namely `/etc/passwd`. The application uses a filesystem API to read and display the content of the file. We can take advantage of that by using path traversal to look for other files.

![pathtraversal1.png](/bok/pathtraversal1.png)

For Windows systems, both ../ and ..\ are valid sequences. An equavalent traversal attack on Windows should look like this:
`?page=..\..\..\windows\win.ini`.

<br />

Using this theory, we are also able to embed websites on the page using a url after the parameter `page=`.

![pathtraversal2.png](/bok/pathtraversal2.png)

Some uses are:
`/etc/passwd` which shows the registered users on the server.
`/proc/version` which shows the OS info of the server.
<br />
<br />




**Command Injection**
Using the ping function on the DVWA website, we can use a semicolon `;` to enter a second line of code within the command. Using this command below, we can find out what user is executing the command.
![commandinjection1.png](/bok/commandinjection1.png)
Here we can see that the user is `www-data`. Without the the command after the semicolon, the command only outputs the results of the ping.

The command `cat /etc/passwd` shows the contents of the file `/etc/passwd` on the linux webserver. the `/etc/passwd` file is used to keep track of every registered user that has access to a system. Getting an output of it gives us more understanding in how the server is structured.
![commandinjection2.png](/bok/commandinjection2.png)

<br />
<br />

# SQL Injection

DVWA starts a bit different from other examples on the internet, but it should do the trick. 
SQL injection (SQLi) is a vulnerability that allows an attacker to interfere with queries to an application's connected database(s). It can give the attacker access to data that should normally not be retrieved. The scope can be any data on the database(s). SQLi attacks have a possibility to escalate to compromising back-end infrastructures and the whole underlying server.

We'll start with some easy examples, categorized in Union-based injections and Error-based injections.

<br />
<br /> 

Union-based injections combine the results from a query with those from the added query (the attack) to extract data. 
Using the SQLi page on DVWA, we can perform a single query where you can find out the first- and last name of a user when entering a user ID. Let's try extracting the passwords!

![sqli1.png](/bok/sqli1.png)

You can notice that the web link gets an ID parameter. Changing that parameter to a different ID will show different results.

We start by adding something extra to the query:
`1 'OR' 1=1`.


by adding `'OR'` we extend the query with the help of our single quotes. We then specify a statement that's always true, say `1=1`. 

The always true scenario is a method to extract more information out of a table. 
When we add the first `1` and we add the 'always true' statement, we don't necessarily have to specify a correct value, because this statement will naturally turn out to be false. We can replace it by '%' or '$' or anything else really, as the value doesn't really matter anymore and we focus on the "always true" statement.

![sqli2-1.png](/bok/sqli2-1.png)
<br />

The next logical step might be to know about the type of database. After all, if you know what database you are dealing with, there are certain common practices, vulnerabilites, known information and bugs that we can make use off. 

`%' or 1=1 union select null, version() #`

![sqli3.png](/bok/sqli3.png)

The `union` command is usable when the application returns a response from the query you make. The `union` command is used to retrieve data from other tables within the database.

Now, we need to extract all the tables so we can pick the right one, using:

`%' and 1=0 union select null, table_name from information_schema.tables #`
<br />

![sqli4.png](/bok/sqli4.png)
<br />

Now that we have the the user table and we know that there is nothing else noteworthy for now, we can proceed to extract all attributes in the user table:

`%' and 1=0 union select null, concat(table_name,0x0a,column_name) from information_schema.columns where table_name = 'users' #`

`concat` adds two or more strings together.

![sqli5-1.png](/bok/sqli5-1.png)

And lastly, reveal the passwords like so:

`%' and 1=0 union select null, concat(first_name,0x0a,last_name,0x0a,user,0x0a,password) from users #`

![sql6.png](/bok/sql6.png)

We extracted hashed passwords from the usertable in the database!

<br />
<br />


# XSS

Cross Site Scripting (XSS) are injection-based attacks that are primarily used by injecting malicious scripts into a part of a website, or in other words, an XSS attack is sending malicious code using a web application. They occur where a user is permitted to use an input and are quite widespread and well-known exploits.

<br />
<br />

## XSS (DOM)

DOM based Cross site Scripting is very similar to Reflected XSS. The difference is that you enter data which modifies the DOM (Document Object Model) of the web page. This data too can contain JavaScript that can be executed on behalf and in the context of the application. What makes it different from Reflected XSS is that by modifying the DOM, the data might never go to the server. If you can find a web-application which relies heavily on client-side JS and makes fast to instant changes to the page you are viewing when you enter data, it's likely that there are scripts to update the DOM.

<br />

On low-security webservers, we can very easily check if the input of the website is vulnerable for XSS. Let's head to the XSS (DOM) section of DVWA and click on the <kbd>SELECT</kbd> key. You'll notice that the URL of the page has changed. It now contains `?default=English`. To check for the vulnerability, we simply need to change *English* to something else, like *Hacking*.
You should now see that the input entry has changed with your value:

![xss1.png](/bok/xss1.png)

<br />

Now that we know we can make use of the vulnerabilities, we can start our exploit. Let's start by displaying a simple alert box. 
As we did before with changing the language entry, we can try changing it to a script line. Something like this:

```html
<script>alert("Hack yeah!")</script>
```

So, the URL should look something like this:
`.../xss_d/?default=<script>alert("Hack yeah!")</script>`

Entering and proceeding with the url gives you a fun alert box.

![xss2.png](/bok/xss2.png)

<br />

This however becomes bored rather quickly. There are other things you can try like extracting cookies or spam-reloading the page, but these things might turn out to be better when we actually store our scripts onto the database. More on that later on. 

**Extract Cookies**
```html
<script>alert(document.cookies)</script>
```


**Spam-reloading website**
```html
<script>window.location.reload()</script>
```

<br />
<br />

## XSS (Reflected)

XSS is a reflected type when you enter data to the application which is immediately echoed back without escaping, sanitization or encoding it. 

Apart from the different usecase/background compared to DOM XSS, it performs the same.
```html
<script>alert("test")</script>
```

![xss2-1.png](/bok/xss2-1.png)

Notice that you even get the same response reflected in the URL, which you can change the same as in the DOM example. 

<br />
<br />

## XSS (Stored)

Stored XSS is, as the name suggests, entering data in the application which will later return in response to another request. The data will contain JS and can be executed not only after a refresh, but also switching/closing tabs. It is a *stored* piece of code after all.
<br />

This is the Stored XSS page of DVWA. 

![xss3-1.png](/bok/xss3-1.png)
<br />

We can figure out where to put our script by just starting to type. You'll notice that the name input is small and has limited characters to type in. The easiest way is typing your script in the message input. If you still come short on your input characters, you can simply try to adjust the amount of allowed characters in the input field as shown below.

![xss3-2-1.png](/bok/xss3-2-1.png)

Now we need to type our script in the message input and put a something irrelevant in the name input and hit <kbd>Sign Guestbook</kbd>

```html
<script>alert("my message :)")</script>
```

An alert box will be shown.
Reloading the page cycles the script through the messages and posts a new one. Now, everytime we go away and come back to the same page, you'll get greeted by the alert box. This means storing our script was successful.

<br />
<br />

# CSRF

CSRF, aka cross-site request forgery, is letting an end user perform a request that they probably don't want/know about. This attack causes the user who clicks on the link to take a certain action with an account whose session ID is stored as a cookie. The link often contains a script to, for example, replace the email address of the account with that of the attacker or to make transactions.

<br />

Using the CSRF page from DVWA, I'll fill in the fields to change my admin password. 

![1.png](/bok/csrf/1.png)

AFter I click on "change" , I can see the following url:
`/vulnerabilities/csrf/?password_new=&password_conf=&Change=Change#`

We'll now try to change the values in "password_new" and "password_conf" to "example01" like so:
`http://192.168.1.21:3006/vulnerabilities/csrf/?password_new=example01&password_conf=example01&Change=Change#`

This works! I get receive a 'password changed' status.

![2.png](/bok/csrf/2.png)

<br />

---

In order to tackle the medium difficulty, let's take a look at the hints first.

> CSRF is an attack that forces an end user to execute unwanted actions on a web application in which they are currently authenticated. With a little help of social engineering (such as sending a link via email/chat), an attacker may force the users of a web application to execute actions of the attacker's choosing.
A successful CSRF exploit can compromise end user data and operation in case of normal user. If the targeted end user is the administrator account, this can compromise the entire web application.
This attack may also be called "XSRF", similar to "Cross Site scripting (XSS)", and they are often used together.

This hint indicates that it has something to do with XSS. I assume that we need to store our new password through an XSS method on the CSRF page. 

I'll use an `img` tag on the XSS stored page as follows:

`<img src='/vulnerabilities/csrf/?password_new=example01&password_conf=example01&Change=Change'>`

After the message has been snent, I can see my image as a comment now:

![3.png](/bok/csrf/3.png)

I used Burp Suite to see my request getting through to the CSRF page. My password is changed.

![4.png](/bok/csrf/4.png)

<br />

CSRF looks a lot like XSS, but still different. You can also use XSS to help with CSRF methods. 

<br />
<br />

---

<br />

# ModSecurityWAF on DVWA

In this section, we'll be taking a look at a WAF for our DVWA instance. A WAF is a Web Application Firewall. They are systems designed to detect and/or block application level attacks on web applications such as SQLi, XSS and command injection. This is precisely what we're trying to accomplish here.

I host my DVWA instance on docker using the image of `vulnerables/web-dvwa`. It is lightweight and has an easy setup. Next, I have installed `ModSecurityWAF`. The full installation guide I used is available [here](https://www.tecmint.com/install-modsecurity-with-apache-on-debian-ubuntu/). In addition to that, I added a fix for a compatibility problem with a particular file that was not included with the instruction. 
Simply execute teh following oneliner:

```bash
sudo mv /etc/modsecurity/rules/REQUEST-922-MULTIPART-ATTACK.conf /etc/modsecurity/rules/REQUEST-922-MULTIPART-ATTACK.conf.renamed
```

Moving on, It's time to test the security of our improved version of DVWA. Let's redo an assignment and see how it would turn out. 
<br />

We'll do some path traversal, and for the sake of simplicity, I'll reuse the same tactics like so:
```
http://192.168.1.21:3006/vulnerabilities/fi/?page=/etc/passwd
```

However, instead of getting our desireable response, I get the following message:

![waf1.png](/bok/waf1.png)

What happened? It seems my web application firewall worked correctly. Let's take a look at the logs using `tail -f /var/log/apache2/error.log` to see how our WAF logs evil actions.

<br />

> *I've organized the logs a bit for better readability. It normally doesn't look like this. The logs shown down below are filtered for the specific scenario.*

<br />



```py
[Tue Jan 10 15:59:36.428012 2023] [:error] [pid 4678] [client 192.168.1.8:2625] [client 192.168.1.8] ModSecurity: 
Warning. Pattern match "(?:^([\\\\d.]+|\\\\[[\\\\da-f:]+\\\\]|[\\\\da-f:]+)(:[\\\\d]+)?$)" at REQUEST_HEADERS:Host. 
    [file "/etc/modsecurity/rules/REQUEST-920-PROTOCOL-ENFORCEMENT.conf"] [line "761"] [id "920350"] 
        [msg "Host header is a numeric IP address"] 
        [data "192.168.1.21:3006"] 
        [severity "WARNING"] 
        [ver "OWASP_CRS/4.0.0-rc1"] 
        [tag "application-multi"] 
        [tag "language-multi"] 
        [tag "platform-multi"] 
        [tag "attack-protocol"] 
        [tag "paranoia-level/1"] 
        [tag "OWASP_CRS"] 
        [tag "capec/1000/210/272"] 
        [tag "PCI/6.5.10"] 
        [hostname "192.168.1.21"] 
        [uri "/vulnerabilities/fi/"] 
        [unique_id "Y72LaKwRAAYAABJGMwoAAAAF"]

[Tue Jan 10 15:59:36.431410 2023] [:error] [pid 4678] [client 192.168.1.8:2625] [client 192.168.1.8] ModSecurity: 
Warning. Matched phrase "etc/passwd" at ARGS:page. 
    [file "/etc/modsecurity/rules/REQUEST-932-APPLICATION-ATTACK-RCE.conf"] [line "524"] [id "932160"] 
        [msg "Remote Command Execution: Unix Shell Code Found"] 
        [data "Matched Data: etc/passwd found within ARGS:page: /etc/passwd"] 
        [severity "CRITICAL"] 
        [ver "OWASP_CRS/4.0.0-rc1"] 
        [tag "application-multi"] 
        [tag "language-shell"] 
        [tag "platform-unix"] 
        [tag "attack-rce"] 
        [tag "paranoia-level/1"] 
        [tag "OWASP_CRS"] 
        [tag "capec/1000/152/248/88"] 
        [tag "PCI/6.5.2"] 
        [hostname "192.168.1.21"] 
        [uri "/vulnerabilities/fi/"] 
        [unique_id "Y72LaKwRAAYAABJGMwoAAAAF"]

[Tue Jan 10 15:59:36.435295 2023] [:error] [pid 4678] [client 192.168.1.8:2625] [client 192.168.1.8] ModSecurity: 
Access denied with code 403 (phase 2). Operator GE matched 5 at TX:blocking_inbound_anomaly_score. 
    [file "/etc/modsecurity/rules/REQUEST-949-BLOCKING-EVALUATION.conf"] [line "184"] [id "949110"] 
        [msg "Inbound Anomaly Score Exceeded (Total Score: 13)"] [
        ver "OWASP_CRS/4.0.0-rc1"] 
        [tag "anomaly-evaluation"] 
        [hostname "192.168.1.21"] 
        [uri "/vulnerabilities/fi/"] 
        [unique_id "Y72LaKwRAAYAABJGMwoAAAAF"]
```

the WAF reported accurately on what happened with detailed information. It reports on the suspicious clients with IP addresses and what they were trying to accomplish. It also records what rule within the WAF is being triggered. With this configuration, this kind of traffic is forbidden and is thus blocked by the WAF. This can be a great enhancement for monitoring when you combine it to a service like Grafana.

<br />
<br />

