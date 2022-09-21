---
title: Project Portfolio  - Research and Notes
description: 
published: true
date: 2022-06-15T09:08:07.598Z
tags: docker, programming, java, s3, portfolio, sdk, jdk, apollo, maven, gradle, rest, graphql, api
editor: markdown
dateCreated: 2022-04-09T22:12:01.594Z
---

# A Beginning

> Deployed application is currently available [HERE](https://myaniview.shiruvaaa.net).
{.is-success}

I also have a group project. Here's a [link](/manuals/s3/group-project) to my documentation!

<br />
<br />

---

I began researching an idea I had in mind. I didn't want to make a generic web shop - that would be boring. I have done this more then once before in different programming languages and I wanted to make something that I could maintain even after this semester (if possible). A project that could be useful in it's own way, even if it was only useful to me. So, I came with an the idea to recreate [Portainer](https://www.portainer.io/) in Java. I have been making use of Portainer for quite some time now and I'm gladly using it to manage my containers, images, stacks and more. But there are some improvements to be made and some personal takes on UX choices which I wanted to change. I made an attempt before in python, and it wasn't all that bad, but working in Python lacks the presence of any straightforward OO-structure in my application,  which I wanted to continue to develop after my last semester when I worked with C#. As I'm more familiar with Python to create small projects, I wanted to learn something new and chose Java this time.

Be that as it may, doing research was a bit harder than I initially thought. I started to look at similar projects, written in multiple languages, as well as reading documentation regarding Docker and Portainer. Unfortunately, I didn't gain much. At a particular point, I came across [documentation](https://docs.docker.com/engine/api/sdk/#unofficial-libraries) which talked about the different Docker Engine SDKs. Docker provides an API for interacting with the Docker daemon, as well as SDKs for Go and Python. The link above contains a list of unofficial libraries which I could use, depending on it's language, maintenance and documentation. The 4 Docker Engine SDKs for Java available provided little to no insight to my understanding in combining a Docker SDK with Java. These SDK's were either no longer maintained, had incredible confusing and/or incomplete documentation or simply didn't meet my requirements (like having the ability to create a list of containers). 

There were more possibilities, like using the official Python SDK and using a script as a mediator between my front- and back-end, but it would eventually take up too much time to research and implement these features. With no optimistic foreseeable future ahead, I decided to think of something else.
<br />



## A new idea
I received a new ~~oracle from god~~ idea while searching the internet in my free time. My idea was to make a combined tracking-overview service, which could gather tracking data from multiple sources and display them together as a portfolio.

To start, I wanted to make use of the [AniList](https://anilist.co/) API to make a personalized web-view of a users own manga/anime progress. It's like your tracking profile in a new coat. I've been using AniList to track what I read or watch for quite some time and have been associating with people that like to do the same. Some of them created their own version of the website or a mobile application, so I have a little backup when it comes to the AniList API. I'm looking forward to it.

<br />

# Learning outcome: Web application
> *You design and build user-friendly, full-stack web applications.*
{.is-info}

<br />

## APIs
I've discovered that the AniList API makes use of a GraphQL API. GraphQL API is a backend API known to be more efficient than REST API when it comes to sending large amounts of data. 

According to [this article](https://blog.api.rakuten.net/graphql-vs-rest/) and [this one](https://www.howtographql.com/basics/1-graphql-is-the-better-rest/), REST stands for representational state transfer. Get and Post are the most common REST operations and very well known among developers. Get and Post are respectively known to gather and send information to the said resources. The second word, "state," stands for statelessness, which means that the server does not store does not store any state about the clients session on the servers side. The session state of the client is kept on the client's side and is responsible for handling and storing session related information on it's own side only. Because of this, REST APIs are known to be less complex. Another positive factor to keep in mind is the structured access to resources, namely in JSON or XML format.

<br />

Now you might wonder what a GraphQL API is. GraphQL is a query language that can be used to work with APIs. GraphQL is seen in the context of a graph, hence the name. 
A REST API is too inflexible when it comes to rapidly changing requirements from the client's side that access them. So, GraphQL came to give an option for more flexibility and efficiency. Where a REST API would gather data from multiple endpoints, you would send a single query to a GraphQL server that includes the concrete data requirements. The server then returns a JSON object with the fulfilled requirements.

After doing a bit of searching, I came across a [sandbox of AniList](https://anilist.co/graphiql?) where I could test my queries with their API. take a look at the example below:

![anilist-graphql-sandbox.png](/s3/portfolio/anilist-graphql-sandbox.png)
<br />

Combine the multiple endpoints that you would use in a REST API and put it in one query to get only the data that you want, without requesting too much or too little. No more over- and under fetching.
<br />

---

In order to create a basic overview of what I had in mind, I made the first layer of a context Diagram.
![context-diagram.png](/s3/portfolio/context-diagram.png)

<br />

## Maven vs Gradle - Short research
What tool is better suited for my project according to my needs? According to [javaatpoint.com](https://www.javatpoint.com/gradle-vs-maven), Gradle as well as maven are both considered standard and widely used amongst developers. While Gradle is a popular build tool for Java, Maven is an older and generally used as an alternative, but can work better with other frameworks such as spring or hibernate. Some key differences between the two are listed below:

<table class="alt" style="width: 692.641px; border: 1px solid rgb(199, 204, 190); text-align: left; display: table; border-collapse: collapse; border-spacing: 0px; color: rgb(51, 51, 51); font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"><tbody style="display: table-row-group;"><tr style="display: table-row; vertical-align: inherit; border-color: inherit; background-color: rgb(239, 241, 235);"><th style="color: rgb(0, 0, 0); background-color: rgb(199, 204, 190); font-size: 17px; font-family: &quot;times new roman&quot;; padding: 12px; vertical-align: top; text-align: left;">Gradle</th><th style="color: rgb(0, 0, 0); background-color: rgb(199, 204, 190); font-size: 17px; font-family: &quot;times new roman&quot;; padding: 12px; vertical-align: top; text-align: left;">Maven</th></tr><tr style="display: table-row; vertical-align: inherit; border-color: inherit; background-color: rgb(255, 255, 255);"><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">It is a build automation system that uses a Groovy-based DSL (domain-specific language )</td><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">It is a software project management system that is primarily used for java projects.</td></tr><tr style="display: table-row; vertical-align: inherit; border-color: inherit; background-color: rgb(239, 241, 235);"><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">It does not use an XML file for declaring the project configuration.</td><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">It uses an XML file for declaring the project, its dependencies, the build order, and its required plugin.</td></tr><tr style="display: table-row; vertical-align: inherit; border-color: inherit; background-color: rgb(255, 255, 255);"><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">It is based on a graph of task dependencies that do the work.</td><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">It is based on the phases of the fixed and linear model.</td></tr><tr style="display: table-row; vertical-align: inherit; border-color: inherit; background-color: rgb(239, 241, 235);"><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">In Gradle, the main goal is to add functionality to the project.</td><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">In maven, the main goal is related to the project phase.</td></tr><tr style="display: table-row; vertical-align: inherit; border-color: inherit; background-color: rgb(255, 255, 255);"><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">It avoids the work by tracking input and output tasks and only runs the tasks that have been changed. Therefore it gives a faster performance.</td><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">It does not use the build cache; thus, its build time is slower than Gradle.</td></tr><tr style="display: table-row; vertical-align: inherit; border-color: inherit; background-color: rgb(239, 241, 235);"><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">Gradle is highly customizable; it provides a wide range of IDE support custom builds.</td><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">Maven has a limited number of parameters and requirements, so customization is a bit complicated.</td></tr><tr style="display: table-row; vertical-align: inherit; border-color: inherit; background-color: rgb(255, 255, 255);"><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">Gradle avoids the compilation of Java.</td><td style="border: 1px solid rgb(199, 204, 190); text-align: justify; padding: 8px; vertical-align: top; font-size: 16px; font-family: inter-regular, system-ui, -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.7; margin-left: 0px; display: table-cell;">The compilation is mandatory in Maven.</td></tr></tbody></table>

<br />

> Gradle is built to overcome the drawbacks of Maven.
{.is-success}

<br />

While Maven has benefits on it's own, like enhanced dependency management, a straightforward debugging process, better co-operation among the source code, plugin, libraries and the IDE and reduction of duplication within the project and there is no need to store the binary libraries (third party) within the source control, but it has it's shortcomings, as it is not the newest tool in the shed.
Gradle's benefits include writing a build script with Java programming language, the support of dependency management, high performance in scalable builds, an easier integration process, multi-project structure support, easier migration from other build tools to Gradle and it is easier to maintain.
<br />

### What's in it for me?
While both choices seemed appealing, the choice was a bit hard to make on my own, so I went and asked some friends that had experience with these tools, and they advised me to use Gradle, as it was a bit simpler to use with GraphQL and dependencies. On to the next issue!

<br />
<br />
<br />



## What now?

My projects idea was to make a combined tracking-overview service, but how would I do that? I mean, GraphQL could be easier used when used straight into a React front-end, as compared to having a Java in-between back-end. It makes the whole ordeal unnecessary. However, by having a Java back-end in between the GraphQL API and the font-end, I can make use of multiple kinds of APIs in the future and collect them through my back-end to re-route them all with the same style to my front-end, making it a more seamless experience. 

<br />

---

I've used C# last semester, so the switch to Java wouldn't be that bad, right? Although most people would think that they're kind of similar, because of their origin, I had a little trouble starting up a project. Most likely due to new terms like Maven, Gradle, things like @Bean, annotations and just regular use cases. 
I've managed to learn basic CRUD functionality with an SQL database and learned some annotations and shortcuts, mostly done through my group-project.

<br />
<br />


## Controller Logic
I want to explore what I found by explaining what I tried to accomplish thus far.
The endpoints of my API are located in the controllers. Let's take a look at an example:

```java
@CrossOrigin(origins = "http://localhost:3000")
@RestController
@RequestMapping("/api/v1/users")
public class MediaListController {
    private final MediaListService mediaListService;

    @Autowired
    public MediaListController(MediaListService mediaListService) {
        this.mediaListService = mediaListService;
    }

    @GetMapping
    public List<Object> listPageItems(){
        return mediaListService.ListPageItems();
    }
}
```

The `@CrossOrigin` is the annotation for permitting cross-origin requests on specific handler classes and/or handler methods. It is processed when a HandlerMapping is used: `@RequestMapping` is used for mapping web requests onto methods in request-handling classes with flexible method signatures.
By using the private final variable, I can access the variable while the value cannot be changed once it is initialized.Next is my constructor, which I mark with `@Autowired` and is apparently an alternative to dependency injection.
Last but not least, I use `@GetMapping` to map HTTP GET requests onto specific handler methods. In this case, a list of objects.

<br />

---

I have to be ready to receive data from a GraphQL API, so I tried using Apollo Client to make a call to a GraphQL service from this Java application. As far as I know at this point, Apollo Client will not just receive some GraphQL data. The first thing to do is creating a query and a schema my application can use. The GraphQL query language is basically about selecting fields on objects. It looks a lot like json, but it's different. My example:

```graphql
query MediaListPage($userName: String, $status: MediaListStatus, $type: MediaType) {
    page: Page {
        mediaList(userName: $userName, status: $status, type: $type) {
            media {
                id
                title {
                    romaji
                    english
                }
                description
                type
                status
                averageScore
            }
        }
    }
}
```

We start by specifying what type of query we want to make. In this case, it's "MediaListPage." This type can be found in the GraphQL schema `schema.graphql`. The `schema.graphql` is a usable blueprint of the GraphQL service that the query depends on. It is also used for Intellisense when writing your GraphQL query. There is a `schema.json` file that displays the GraphQL query types in json format and last but not least, we got a `graphql.config`, which defines the GraphQL server and defines other data, like headers.

So now that we've gotten a hold of the GraphQL API, we need to process the query and receive a proper response. Apollo-Client is a way to do this.

```java
@Repository
public class MediaListRepo {
    private ApolloClient apolloClient;

    @Autowired
    public MediaListRepo(ApolloClient apolloClient) {
        this.apolloClient = apolloClient;
    }

    
    public MediaListPageQuery.Data GetMediaListPageData(MediaListPageQuery mediaListPageQuery) throws ExecutionException, InterruptedException {  
        var call = apolloClient.query(mediaListPageQuery);
        var future = CompletableFutureUtils.toCompletableFuture(call);
        var results = future.get();
        return results.getData();
    }
}
```

`//MediaListPageQuery`: (Assuming that we have to wait for data (async)).  - This is the auto-created query made by Apollo, grabs the GraphQL query data and passes it through the function.

`//var call`: creates a new Apollo query call -- magic container

`//var future`: used for asynchronous computation, combinable with other stepsa future represents what you want to do in a later point in time. future.get() waits for the current thread and while executing others.

`//results` gets the results of future: asynchronous computation

<br />



## Java and Apollo Client

I got more experience with Java and GraphQL. 
Basically, it's all just a pain ~~in the ass~~. Other tools for making calls to a GraphQL service inside an application, especially Java, are almost non-existent. If there are any, they're either poorly documented, outdated or just not suited for the things I want to use, which ultimately made me deal with Apollo Client.

![apollo-client-view.png](/s3/portfolio/apollo-client-view.png)
<br />

After various attempts in searching for another possibility, I pushed myself back to Apollo Client. You see, Apollo Client shouldn't be that bad. It is more used, has up-to-date documentation and should be easier than any other solution I've come across. Unfortunately, Apollo Client is not fully optimized for Java, as seen in the documentation. You can see in the picture above that Apollo Client is either available in React, iOS or Kotlin. 
As Kotlin came fairly close to Java, it was my only lead to build on that. I looked up many examples, watched videos and compared documentation, but to no avail. There is one page in the Kotlin documentation about Java which says the following, and I quote:

> Apollo Kotlin has a coroutines / Flow-based API that isn't well suited to using with Java.



Amazing.Though I have tried to create something out thin air (Kotlin), I just couldn't figure out how to work with it.

<br />

---


I'm trying Apollo Client In React right now but it didn't go as smooth in the beginning and it certainly isn't going any better now.

Seriously, Apollo Client has full support in React, but it can't handle React 18, which is the latest version of of React... Furthermore, as the documentation was not that great, I had to find a YouTube video (again) to educate myself on the pains of GraphQL calls. Most of these videos use outdated packages. 

At this point, I'm seriously considering creating microservices, just so that I don't have to deal with the unnecessary complication. I'll do some separate research on that. Should I try Kotlin as well?

<br />


## GraphQL - A breakthrough

So, cool things happened. I finally got the process down on how to get GraphQL queries working within my application. I shifted my focus entirely on React to simplify the process and start out from there. 

After watching many videos and reading more manuals, I finally managed to get a better understanding on the implementation I needed to do in order for GraphQL to work. I got to learn about queries, Apollo-Client, GraphQL (in combination with custom queries and variables) React, Hooks, JS and more! After finally getting back some data, I got excited again and developing went a bit smoother.

---

<br />


I want to break down what I have so far, but I won't go into too much detail, as it'll get too much to read.

I started with basic functionality (`index.js` & `app.js`) by adding the data provider with apollo and some routes. Next, I began my first GraphQL query by requesting a list of manga:

```graphql
{
  Page(perPage: 10){
    media( type: MANGA) {
      id,
      title {
        romaji
        english
      }
      coverImage {
        medium
      }
    }
  }
}
```

This query requests all manga from the website in batches of 10 per page (pagination not included yet). It requests things like an id, different kinds of titles and a cover image. I made a data function with it to display my fetched data and decided to split my functionality in multiple files. \

I started working with Hooks and discovered that they were less difficult than I had anticipated. I transfered my query in my hook which now looks somewhat like this:

```js
import { useQuery, gql } from '@apollo/client'

const GET_MANGA = gql`
{
  Page(perPage: 10){
    media( type: MANGA) {
      id,
      title {
        romaji
        english
      }
      coverImage {
        medium
      }
    }
  }
}
`

export const useMangaList = () => {
    const { error, data, loading } = useQuery(GET_MANGA);
    // dir > log for non-string console messages.
    // console.dir({ error, loading, data });
    return {
        error,
        data,
        loading,
    }
}
```

Next to my hook, I needed a page to display my fetched data from my hook. By using the exported value `data`, I could then call data from that variable in another file like so:

```js
import React from 'react';
import { useMangaList } from '../Hooks/useMangaList';
import second from '../../../img/loading.gif'

export default function MangaList() {
  const {error, loading, data } = useMangaList();
  if (loading) return <img src={second} alt='loadinggif'></img>;
  if (error) return <div>Whoops! Something went wrong...</div>

  return <div className="MangaList">
    {data.Page.media.map(manga => {
      return <div key={manga.id}>        
          <h2><b>English: </b>{manga.title.romaji}</h2>
          <img src={manga.coverImage.medium} alt='Cover' />
        </div>
    })}
  </div>;
}
```

For displaying, it was just a matter of mapping out my data.

<br />

# Learning outcome: CI/CD
> *You design and implement a (semi)automated software release process that matches the needs of the project context.* <br />
{.is-info}

My CI/CD section can be found in a seperate file [here](/manuals/CI-CD).

I designed a release process with the help of scripts running on Github to deploy packages for automatic docker images. The code on which these images will be based on are monitored through Dependabot and Sonarcloud. Tests makes sure functions actually work. More on tests below.

<br />
<br />

# Learning outcome: Software quality
> *You use software tooling and methodology that continuously monitors and improve the software quality during software development.*
{.is-info}

<br />

## Async Testing - Short research

See [Async Testing](/manuals/s3/Async) for more information about experimenting with asynchronous thread testing. 
<br />

An honorable mention to [CI/CD](/manuals/CI-CD), because this covers '*continuously monitoring and improving software quality during development.*'

## Straight Code Testing

Testing in JavaScript is pretty straightforward. I have divided my tests in two seperate folders. One for local user data and one for the AniList GraphQL api. 
![test-folder.png](/s3/test-folder.png)

I used a few simple tests to check if api responses turned out to be defined. All in all, not very dramatic.
![test-results.png](/s3/test-results.png)

<br />

As for Java, I had a little more trouble setting up the tests, but it turned out okay in the end.
Below is an example on a test where it compares given data from an SQL file within the H2 database with fixed values.
```java
class UserControllerTest {

    @Autowired
    MockMvc mockMvc;

    @Test
    @Sql("/test-data.sql")
    public void getAllUsers() throws Exception{
        mockMvc.perform(MockMvcRequestBuilders.get("/api/users")
                        .contentType(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$[0].id").value(1))
                .andExpect(jsonPath("$[0].username").value("admin"))
                .andReturn();
    }
}
```
This setup uses a seperate `.properties` file to configure the tests stand-alone and accurately.

<br />