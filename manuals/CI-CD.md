---
title: CI/CD - A Simple Overview
description: 
published: true
date: 2022-06-15T08:48:40.723Z
tags: 
editor: markdown
dateCreated: 2022-04-20T14:25:48.680Z
---

> __[Learning outcomes: 4. CI/CD]__
*You design and implement a (semi)automated software release process that matches the needs of the project context.* <br />
I designed a release process with the help of scripts running on Github to deploy packages for automatic docker images. The code on which these images will be based on are monitored through Dependabot and Sonarcloud. Tests makes sure functions actually work.
{.is-info}

<br />

CI/CD is a method to frequently deliver apps to customers by introducing automation into the stages of app development. The main concepts revolve around continuous integration, continuous delivery, and continuous deployment. CI/CD is a solution to the problems integrating new code can cause for development and operations teams (AKA "integration hell"). So basically, CI/CD can solve a lot of problems by automating a lot of manual work. For more information, click [here](https://docs.github.com/en/actions).
CI/CD is pretty neat.

<br />
<br />

## A Walkthrough
Alright, to experience it first-hand, we'll go through a project of mine: https://github.com/silverfs/myaniview-r

<br />

### CI (Continuous Integration)

Let's start with in-built functions on Github. These are functions anyone can use out of the box. 
There are some options to choose from, but the things I will be focussing on, are Dependabot functions.
![git-analysis.png](/cicd/git-analysis.png)

It's as simple as enabling them in your project settings. Dependabot will alert you on critical coding errors and vulnerabilities (be it code or packages you use). It can even make pull requests to bump up versions of vulnerable packages, which makes automatic code-checking a walk in the park.

<br />

**Sonarcloud**

Speaking of code-checking, I integrated my project with [Sonarcloud](https://sonarcloud.io/). I helps maintaining a clean repo and checks for bugs, code smells, vulnerabilities and security hotspots! You can configure a dashboard per project and even per branch, whatever suits your tastes. Here's how my dashboard looks like (or click on the image to view the curren dashboard):

[![sonar.png](/cicd/sonar.png)](https://sonarcloud.io/project/overview?id=silverfs_myaniview-r)

I synced my Sonarcloud with Github Actions. This is my [Sonarcloud configuration](https://github.com/silverfs/myaniview-r/blob/master/.github/workflows/sonarcloud.yml).

<br />
<br />

### CD (Continuous Deployment)

Okay, let's head to the project repository again. You can find a tab called ![gh-actions.png](/cicd/gh-actions.png) as one of the tabs and is generally found on almost any Github project. It will show you something like this:


![github-workflow.png](/cicd/gh-workflow.png)


Now, how did I get here? To get our successful workflow-runs, we'll need to have a basic understanding of Docker first. You can read more about Docker [here](/manuals/docker).
I made a Dockerfile in the root folder of my project to build an image of my application. 
This is how it looks like:

```Dockerfile
FROM node:alpine
WORKDIR /app
COPY . .
RUN npm i
RUN npm run build
CMD [ "npm", "start" ]
```
Now that my Dockerfile is in my rootfolder, I'll have to create a workflow to automate the process of building my image and sending it to [Github Packages](https://ghcr.io) so my image will be usable/downloadable accross the world.

![publish-container.png](/cicd/publish-container.png)

The workflow "Publish Docker Container" creates a file in [/.github/workflows](https://github.com/silverfs/myaniview-r/blob/master/.github/workflows/docker-publish.yml) with a YAML script that'll execute everytime a change has been made to the branch/image. The file specifies when and where the execution will take place and how it should behave. This script ultimately publishes the package to Github Packages. You can verify it [here](https://github.com/silverfs/myaniview-r/pkgs/container/myaniview-r).


<br />

After the package is successfully created, we can then use the image file in a docker-compose file to deploy the container locally, e.g.:


```yaml
# docker-compose.yml

version: '3.3'
services:
  app:
    image: ghcr.io/silverfs/myaniview-r:master
    restart: unless-stopped
    ports: 
      - 3010:3000
```

<br />

---

<br />

### Backend gp

As the backend of my group-project is almost the same as my personal project, I'll continue from there for the backend. All in all, the [backend of our group-project](https://github.com/RensvGemert/S3-GP-Backend) is Java with a MySQL database and is also published as a docker container to ghcr.io.
There is a docker-compose file which makes use of the published packages on Github:

```yml
version: '3.3'
services:
  pimdatabase:
    image: mysql
    networks:
      - pimnetwork
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=password
      - MYSQL_DATABASE=pimdatabase
    ports:
      - 3306:3306
    volumes:
      - my-db:/var/lib/mysql
  frontend:
    image: ghcr.io/rensvgemert/s3-gp-frontend:master
    restart: always
    ports: 
      - 3001:3000
  backend: 
    image: ghcr.io/rensvgemert/s3-gp-backend:main
    ports:
      - 8080:8080
    networks:
      - pimnetwork
    depends_on:
      - pimdatabase
    restart: always
    environment:
      SPRING_APPLICATION_JSON: '{
        "spring.datasource.url"  : "jdbc:mysql://pimdatabase/pimdatabase",
        "spring.datasource.username" : "root",
        "spring.datasource.password" : "password",
        "spring.jpa.properties.hibernate.dialect" : "org.hibernate.dialect.MySQL5InnoDBDialect",
        "spring.jpa.hibernate.ddl-auto" : "update"
        }'
# Names our volume
volumes:
  my-db:
networks:
  pimnetwork: 
```

THe yaml file is split into 3 sections, namely the frontend, backend and a database.
Notice that the backend has some extra environmental variables. These are meant to set change the password and username of the mysql database, or change the datasource url if feel that is necessary.

The backend itself has two workflows:
![backend-workflows.png](/cicd/backend-workflows.png)
Docker publish and Java CI with Maven.
The Docker workflow is meant to publish a package which we can use in our stack.
The Java CI is meant to build the project as a package, which runs tests on it as well:


```yml
# This workflow will build a Java project with Maven, and cache/restore any dependencies to improve the workflow execution time
# For more information see: https://help.github.com/actions/language-and-framework-guides/building-and-testing-java-with-maven

name: Java CI with Maven

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Set up JDK 17
      uses: actions/setup-java@v3
      with:
        java-version: '17'
        distribution: 'temurin'
        cache: maven
    - name: Build with Maven
      run: mvn -B package --file pom.xml
```
These tests run with the build function. When a test fails, a portion of the Java CI failes as well.
![java-tests.png](/cicd/java-tests.png)
It is shown here that those containers run with their own packages.
![image.png](/cicd/image.png)