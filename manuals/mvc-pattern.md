---
title: MVC Architectural Pattern
description: 
published: true
date: 2022-04-20T14:20:17.078Z
tags: programming, mvc, mvc-pattern, web development
editor: markdown
dateCreated: 2021-09-07T20:42:38.973Z
---



MVC is the most popular architecture for building complex web servers. It is used by many frameworks, and implemented into nearly every modern web application. It was originally designed for desktop applications, but now it is widely adopted in web applications and others. MVC stands for Model, View, Controller. The goal of this pattern, is to split a large application into specific sections that all have their own purpose, to handle large and/or difficult applications easier.


</br>

## Model

In an MVC application, a model represents the application data and behaviour in terms of its problem domain and independent of the UI. A model will consist out of one or multiple classes. These classes contain propperties and methods that represents the application state and rules. They are not tied to the UI, which means that you can take these classes and use them in different kinds of apps, like in desktop or mobile environments.
Models are "[Plain Old CLR Objects](https://en.wikipedia.org/wiki/Plain_old_CLR_object)" (POCOs).

</br>

## View

The View handles presenting the information. It will usually render dynamic HTML pages based on the data the model fetches. The Controller is responsible for passing that data between the Model and View, so that the Model and View never have to interact with each other. So, the view is essentially the HTML markup that you display to the user.

</br>

## Controller

The controller is responsible for handling an HTTP request (a user request). Let's say an application is hosted on https://shiruvaaa.net. When we send a request to https://shiruvaaa.net/things, a controller will be selected to handle it's request. Now as an example, this controller will get data from a database, put the data in a view and return the view to the client/browser.

</br>