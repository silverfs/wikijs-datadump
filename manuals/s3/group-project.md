---
title: Piada PIM - WoC Group Project
description: 
published: true
date: 2022-06-15T11:29:30.257Z
tags: 
editor: markdown
dateCreated: 2022-04-14T13:36:33.922Z
---

# Introduction

WoC ([World of Content](https://worldofcontent.com/en-gb/)) has given us, S3-DB02-1, the mission to create a mini [PIM](https://www.informatica.com/resources/articles/what-is-product-information-management.html) to our liking. We received some general information about WoC and started brainstorming from there.

We chose to focus on competition. This means the following:
<br />

### Starting with the suppliers:

the supplier (e.g. Sligro) has products that they want to sell. In order to sell to as many suppliers as possible, Sligro puts its products on our platform. There are many retailers on this system. For retailers, this is a great platform with a wide choice of products from different suppliers. This means a lot of competition between different suppliers.
<br />
### Retailers:

The retailer (e.g. Jumbo) is looking for products. On this platform, Jumbo has a choice of different products with different brands, prices and stockpile. Jumbo uses this platform to make good choices between different suppliers.
<br />
### Site Admins:

In addition to these 2 important roles, we naturally have the site owners (e.g. superadmins and more). They can also function as the staff of the PIM system. To give you an example: staff can provide customer support for both customers for problems and questions about the platform. Although this is important, we will focus less on this part.
<br />

All customers - suppliers and retailers - must have an account to access the platform's content. When creating an account, they can choose which role they have. If the customer chooses the retailer role, they will have access to all suppliers and retailers on the platform. The suppliers for what they deliver, and the retailers to, for example, look at basic statistics of others. A supplier will also have to be able to view the statistics of other suppliers in order to adjust its own, such as prices and delivery updates.

Next up --> [Trello](https://trello.com/b/Q4D0RcQU/proftaak-semester-3).

<br />
<br />

## Java.. but why?
There were no specific requirements on a programming language set by WoC, so we were free to chose our own.
We chose Java as we wanted to learn a new programming language. We mainly used C# in our previous year and as Java has a logical affiliation with C#, we started to look more into it.
Today, Java is one of the most popular programming languages. It powers enterprise web apps, big data pipelines, mobile apps on android and more. Java has a "write once, run everywhere" flexibility that is far more beneficial than one might expect. Instead of compiling to machine-code, like C or C++, it compiles to byte-code, that can run on any operating system without recompiling. Java uses a Java Virtual Machine (JVM) to execute and the machine in question just needs the Java Runtime Environment (JRE) installed.

As Java is so widely used, support for this programming language is not hard to find. Furthermore, Starting with Java, a project can be easily converted to Kotlin.

As almost all our group members plan on using Java in their individual project, it can help in troubleshooting both sides and enhance our productivity.

It has been agreed upon that we would use **Maven** in our project, as Maven is generally more known amongst fellow devs and thus easier for finding things on the internet. Click [here](/manuals/s3/portfolio#maven-vs-gradle) for a simple overview on differences between Maven and Gradle.
<br />
<br />


## React
*Credits to Fireship:*

[![IMAGE_ALT](https://img.youtube.com/vi/Tn6-PIqc4UM/0.jpg)](https://youtu.be/Tn6-PIqc4UM)

<br />

The reason we chose React is due to it's logical building process and it's simplicity. The use of JSX, which allows us to combine JavaScript with html markup, makes the building of a component - which is basically just a JS function - a piece of cake.
The changing of values within React makes it easy to debug outcomes and data within the UI.
Furthermore, React has a massive ecosystem, which consists of open-source components from the community for every situation possible.

<br />

# Learning outcome: Web application
> __[Learning outcomes: 1. Web application]__
*You apply basic User experience testing and development techniques.*
{.is-info}


We chose to work with a central framework to minimalise the irritation in user experience. By using a framework like React-Admin, we centralized theming and common practices to make a cleaner and more user friendly experience.
We made sure to take small things into account, like user errors and commonly made mistakes made by end-users by implementing a framework and policies that takes care of all of these things. More on this down below.

## Frameworks

Speaking of React, I've come accross a neat framework called [React-Admin](https://marmelab.com/react-admin/) which we eventually used as a replacement for bootstrap inconveniences. I must say, React-Admin is pretty amazing. It takes so little effort to create a constructed overview with multiple functions. That is, if you have everything figured out... The only downside is that some features are under the enterprise-edition, thus paid. Most of the functions that we can use work just fine. This framework takes care of a lot of UX problems, like inconvenient styling, familiar design patterns and more.
<br />

The basics happen in the app.js file. 
This is where all the ~~magic~~ combining happens. Let's take a direct look at the app.js from [our project](https://github.com/RensvGemert/S3-GP-Frontend):

```js
import * as React from "react";
import { Admin, Resource, fetchUtils, ListGuesser, List } from 'react-admin';
import jsonServerProvider from 'ra-data-json-server';
import ProductList from './components/ProductList'
import UserList from "./components/UserList";
import UserEdit from "./components/UserEdit";
import ProductEdit from "./components/ProductEdit";
import UserCreate from "./components/UserCreate";
import ProductCreate from "./components/ProductCreate";
import simpleRestProvider from 'ra-data-simple-rest';

const fetchJson = (url, options = {}) => {
    if (!options.headers) {
        options.headers = new Headers({ Accept: 'application/json' });
    }
    // add your own headers here
    options.headers.set('Access-Control-Allow-Origin', '*');
    return fetchUtils.fetchJson(url, options);
}

const dataProvider = jsonServerProvider('http://localhost:8080/api', fetchJson);

const App = () => (
    <Admin dataProvider={dataProvider}>
        <Resource name="users" list={UserList} edit={UserEdit} create={UserCreate} />
        <Resource name="products" list={ProductList} edit={ProductEdit} create={ProductCreate} />
    </Admin>
);

export default App;
```
<br />

Let's slice it up a little.

Let us import all the basic stuff (React and of course React-Admin) and a dataprovider.
The most basic and simple app.js structure would look somewhat like this:

```js
import * as React from "react";
import { Admin, Resource, List } from 'react-admin';
import UserList from "./components/UserList";

const dataProvider = jsonServerProvider('http://localhost:8080/api');

const App = () => (
    <Admin dataProvider={dataProvider}>
        <Resource name="users" list={UserList} />
    </Admin>
);

export default App;
```
This structure needs only a few lines of code to create a base for a automated constructed table (UserList). It is exactly works like it shows. 

You start with the dataProvider: the head-URL of your API.
Now add that to your "Admin" and add your first Resource - in this case, "users". The name of the resource is equal to the endpoint of your datProvider API. The last thing we need to address is the extra functionality you can add to a resource. Here, we added "UserList" as a list. This list get's created as a table on our page. But how does it do that? Surely this isn't all?

That's right, it isn't. As you can see at the 3rd import line, "UserList" refers to a specific component I created while you were reading this. Let's take a look at it, shall we?
<br />


```js
import React from 'react'
import { List, Datagrid, TextField, EditButton, DeleteButton, Filter, SearchInput } from 'react-admin'

const UserFilter = (props) => (<Filter {...props}>
  <SearchInput placeholder='User Email' source='email' resettable alwaysOn />
</Filter>)

function UserList(props) {
  return (
    <List {...props} filters={<UserFilter />}>
        <Datagrid>
            <TextField source='id' />
            <TextField source='name' />
            <TextField source='email' />
            <EditButton basePath='/users' />
            <DeleteButton basePath='/users' />
        </Datagrid>
    </List>
  );
  
}

export default UserList
```
The cool thing about creating components like this, is that it takes the direct properties from your API endpoint (Resource, e.g.: http://localhost:8080/api/users) so you can map them easily inside specific field in your datagrid. Your datagrid is a table that renders according to your entries in your API endpoint. Of course, we can add more functionality, like an edit- and delete button, a data-filter and even different types of fields, like RichTextFields and ImageFields.

<br />
<br />


As expected, not everything went according to plan with this approach. More on that in the next section. 

## Back-end

Now let's talk a litle about Java. [Our back-end](https://github.com/RensvGemert/S3-GP-Backend) uses Spring-Boot 2.6.4. We began to set up a basic implementation of Spring web application - MVC - with the hulp of some planning. By talking with the customer, World of Content and some brainstorming, we came with some plans to start our work.

![](https://media.discordapp.net/attachments/940529481184083968/965899021061353472/IMG_20220419_105737.jpg)


Next to automated table-creation in the database, we used the classic MVC workflow to power our backend API. 

As it is too much to show you a complete workflow, I'll be showing the most important parts that differentiate it from other things.

It took a while to fix, but we were stuck on api headers for quite a while. You see, React-Admin requires you to include a total-count header in your API endpoints. The total-count is needed to paginate the React-Admin tables and it took quite some time to correctly add the right headers to the api in the back-end. We put this in a special class:

```java
@ControllerAdvice
public class ResourceSizeAdvice implements ResponseBodyAdvice<Collection<?>> {
    @Override
    public boolean supports(MethodParameter returnType, Class<? extends HttpMessageConverter<?>> converterType) {
        //Checks if this advice is applicable.
        //In this case it applies to any endpoint which returns a collection.
        return Collection.class.isAssignableFrom(returnType.getParameterType());
    }


    @Override
    public Collection<?> beforeBodyWrite(Collection<?> body, MethodParameter returnType, MediaType selectedContentType, Class<? extends HttpMessageConverter<?>> selectedConverterType, ServerHttpRequest request, ServerHttpResponse response) {
        response.getHeaders().add("Access-Control-Allow-Methods", "POST, GET, PUT, UPDATE, OPTIONS");
        response.getHeaders().add("x-total-count", String.valueOf(body.size()));
        response.getHeaders().add("access-control-expose-headers", "X-Total-Count");
        return body;
    }
}
```

The problem was being solved by adding an extra file to override the API controller in the Java back-end to include certain headers in the API headers. This however does not mean pagination is 100% functional. More on that later in the 'filter' section.

<br />

Every controller has seperate request mappings to serve requests from the client. We divide controllers like 'products' or 'users' in seperate 'companies' so everything is clear from confusion and is thus easier to work with, including authorization. 

```java
@CrossOrigin(origins = "*")
@RestController
@RequestMapping("/api/company/{companyId}/products")
public class ProductController {
```






<br />
<br />
<br />
<br />

# Learning outcome: Agile
> You are aware of the most popular agile methods and their underlying agile principles.
{.is-info}

From the beginning of our project, we aimed to work with agile methods to enhance our collaboration and work effectiveness. 
Our group chose to try out the scrum method while realizing and developing our project. We chose to follow a pre-defined set of rules, like doing a stand up around 9:30 every project day. This standup included a personal description around the table about the activities that we did the project-day before, activities what we will be working on today and other things to take note of. We used a [Trello board](https://trello.com/b/Q4D0RcQU/proftaak-semester-3) to manage our user stories and activity features to split up our workforces in an efficient way and to create a good workflow and overview of the project.

We did a reflection, both personal but mostly in the group, about the most recent sprint after every prototype delivery. We discussed what went great and what could be better and wrote these things down to reflect and improve on our next sprint.


<br />

<img src='https://cdn.discordapp.com/attachments/940529481184083968/963370431052677190/IMG_20220412_112947.jpg?size=4096' height=500 />
<img src='https://cdn.discordapp.com/attachments/940529481184083968/978667641839435816/PXL_20220524_163525176.jpg?size=4096' height=500 />



<br />

## What does it mean to work agile?

According to [Bit](https://www.bit.com.au/guide/what-is-agile-how-it-actually-works-457412) -  
> "agile working prioritises speed of delivery, colaboration between different business units and adaptability over more traditional aproaches such as ['waterfall'](https://www.umsl.edu/~hugheyd/is6840/waterfall.html) " 

(also called the traditional technique, popular as linear methodology).

I view agile more as a team-based approach and a great example of this is using scrum. The scrum methodology is a repeating cycle that represents how a team can, for example, develop an application dynamically, with a less 'structured' approach. No more traditional planning and documentation. 
<br />
## The difference between waterfall and agile
As we are talking about agile, let's highlight it's characteristics:
Working agile is in conitnuous cycles. It's can work for all, but works better for small, high-functioning and collaborative teams. As it is in continuous, it tends to be more flexible. One last note, it involves more customer involvement. 

Now, the Waterfall method on the other hand works less in cycles and thus has a more sequential approach. It's planning doesn't evolve that much with the project but is more upfront. This type of workflow works better for simple and unchanging projects.
 <br />

<img src='https://kanbanize.com/wp-content/uploads/website-images/Agile/traditional_vs_agile_planning.png' height=350 />

<br />

## What did I think about working agile in our project?
Working with scrum went great. My teammates performed really well in both teamwork, agile working and flexibility. Working with an agile system brings a more structured work pattern and it can, with good monitoring, come out quite nice. We did start a bit awkward on agile terms, but after a short while, it gradually became better.

<br />
<br />


# Learning outcome: Business process
> Involving stakeholders, predominantly sequential processes with one or two alternative paths.
You have analyzed and modeled an existing business process from your project prior to the introduction of the software that you are creating.
{.is-info}

<br />

My project is far too small to create a proper business process out of it. Instead, I'll just talk about it by answering a few of the questions provided by the learning outcome with some examples.

***What is a business process?***
"*A business process is a collection of business tasks and activities that when performed by people or systems in a structured course, produces an outcome that contributes to business goals." --> [(source)](https://blog.processology.net/what-is-a-business-process)*

***How does a business process relate to software applications?***
As a business process is a set of activities that accomplish a specific (organizational) goal, it is not limited to certain topics.
Business process management can be viewed in different lights. Some take it in steps of five, others in 8 or 10. But the basics, including related to sofware development, comes down to some basic things:

"*Software development starts with planning and analysis of the requirements. The follow-up steps include documenting the requirements and the timeline in a structured format. Once the documentation is ready, the design and prototyping of the application take place, followed by the actual development process. Testing and Deployment are important steps that either go along with the development cycle or happen at the end of every module completion." --> [(source)](https://itchronicles.com/business-process-management/business-process-management-in-software-companies/)*

To understand and visualize what this article wrote about, I have drawn out the process above to further elaborate the source-text:

<img src='/s3/business-process.png' height=400 />
<br />
You 'start' the cycle at the middle-left oval. I've drawn the process in an endless circle, but it doesn't neccesarily have to be endless. For example, as the article mentioned:

"*Testing and Deployment are important steps that either go along with the development cycle or happen at the end of every module completion".* 
This means it can be applied to more than one methodology (like agile or waterfall).

<br />
<br />

This might not have given enough clarity on the subject, so let me insert an example of a business process from a company where I used to work. It is a trampoline park where in context, the staff described is the staff from the company and the customer is the person who is caling to make a reservation. The whole process is done through a phone-call. Unlike the process above, nothing here is automated.

<img src='/s3/process-3.png' height=400 />


<br />



# Learning outcome: Requirement & Design
> You apply user acceptance testing and stakeholder feedback to validate the quality of the requirements. You evaluate the quality of the design (e.g., by testing or prototyping) taking into account the formulated quality properties like security and performance.
{.is-info}

After our first call (meeting) with WoC and doing the necessities, we started noting down our user stories and began to prioritize them. This may sound simple, but we had a lot to think about. What the customer expects us to make, how filter out the most important features, taking the future application user into account and more. We made some sketches, models and brainstormed alot to come up with ideas that were in the project's scope and still feasible. Then it was just a matter of splitting up the user stories and start development. With every comeback every 3 weeks, we took our time to ask more questions, review our user stories and plans for the future, and noticably tweaked our planning and notes in accordance to the conversations we held with the customer WoC.

<br />

Below are our first created user stories:

<img src='https://media.discordapp.net/attachments/940529481184083968/945688070831890483/IMG_20220222_152630.jpg' height=500 />

We process these user stories in our Trello board. This is an example of a finished feature:
![userstory.png](/s3/userstory.png)

And with a lot of brainstorming, we came with a database idea that might work with our project:


<img src='https://media.discordapp.net/attachments/940529481184083968/965899021061353472/IMG_20220419_105737.jpg' height=400 />

And, of course, we had to design a simple user structure as well: 

<img src='https://cdn.discordapp.com/attachments/940529481184083968/953219902993494056/Conceptueel_model_PIM_Piada.jpg?size=4096' height=400 />

<br />

The whole class did a prototype showcase + review per projectgroup to check out each other's projects, to notice what could be better with your own project and to learn from the other groups. We took this event as our chance to check out some design flaws, both in software as well as . People noticed some contrast text that could be better, as well as some not-working elements, like pagination, that we could hide from the average user. We took this with us as valuable information and improved our actions.

<br />


# Learning outcome: Cultural differences and ethics
> You recognize and take into account cultural differences between project stakeholders and ethical aspects in software development.
{.is-info}

It is only natural that as technologists, we spend most of our time focusing on how our tech will change the world for the better. Which is great. Everyone loves a sunny disposition. But perhaps it’s more useful, in some ways, to consider our glass half empty. What if, in addition to fantasizing about how our tech will save the world, we spent some time dreading all the ways it might, possibly, perhaps, just maybe, screw everything up? The last thing you want is for your optimism to create blind spots around the possible downsides of your tech.

<br />

I've picked a definition from [this source](https://www.merriam-webster.com/dictionary/culture) for the word 'culture':
"*The characteristic features of everyday existence (such as diversions or a way of life) shared by people in a place or time.*" 

This can apply to both groups of people as well as individuals. I have chosen this explanation above others, because for me, this describes what culture means in broader terms and is not necessarily bound to any other terms. 
<br />

## But what does this have to do with software engineering?
Well, as all people are advancing in a different way,there obviously is not only one way to do things. This also applies to customs in the software engineering world.
Not only can people experience differences in language, but also the way they code, write documentation, customs in writing software, etc.

Personally, I have had multiple encounters with people from different cultures and that's still happening to this day. Not only within the school boundaries, but often online, where I have friends from around the world which have different kinds of knowledge about customs, writing code and experiences. I have never had any problems with this approach and enjoyed the difference in experience. After all, I learned quite a lot with an approach like this.
But also in my own project-group do we have different backgrounds in experience and customs, even though we study at the same school, which makes programming more fun.

<br />

To tell something about ethics, we first need to understand what it actually means.

People seem to misunderstand the difference between morals and ethics. While morals are the understandings of right and wrong, ethics is the principle behind it. How you came to that conclusion. Ethics are reasons for an action. [(source)](https://www.britannica.com/topic/ethics-philosophy)
<br />


With the help of the [TICT tool](https://fhict.instructure.com/courses/12077/files/1574771/), my project-group and I have brainstormed about the possibilities on applying certain ethical subjects within our project. 

<img src='https://media.discordapp.net/attachments/940529481184083968/982210474689069129/PXL_20220603_111310959.jpg' height=500 />

The subjects I think are most important in developing software in general and in regards to ethics are privacy and sustainability. Privacy covers a lot more than just it's main subject. It can include transparency, fairness and data. It's a broad term that packs a lot of functional goodness.
Sustainability is needed for maintainability - including the privacy part - and works together with future thinking.
<br />

## How this involves our project situation
As to how these subjects are involved in our project, you'll have to take a look at the picture above. We did a brainstorm session about each individual part on the tool and explained/wrote down our visions underneath. 
As we wrote down our thoughts, conflicts naturally arose. Subjects like bad actors and data made us all the more realise that security wasn't our strongest point in our project and could be greatly improved.

Although we haven't completely made a thorough plan about it, we try to keep our application as fair as possible. Being as transparent as possible, making everything open source and using packages and frameworks that are trusted, maintained and FOSS are important to us. Furthermore, we don't use tracking, be it account-bound or personal data and are not planning to implement these kinds of functions in the near future. Data that we possess is not being sold to anyone. 
<br />

## Why is this all important?

As your project eventually's getting used by not only consumers but potentially other developers, it has the possibility to have a great impact, be it good or bad, on people. 
The sentence "*with great power comes great responsibility*" can be used in this case more than I had anticipated. Even though you can create an application with good intentions, you have to be aware of the possible influentual consequences while you continuously develop and maintain your application. This applies in both the software and the mental state behind the application itself. Make sure your product is used as intended by the people that use your software.