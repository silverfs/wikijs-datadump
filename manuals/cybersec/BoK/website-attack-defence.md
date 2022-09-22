---
title: Web Security Attack and Defence
description: 
published: true
date: 2022-09-22T14:51:52.558Z
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

<br />]

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


# XSS & CSRF

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