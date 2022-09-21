---
title: Async Testing
description: 
published: true
date: 2022-06-15T09:08:40.957Z
tags: async, sync, asynchronous, synchronous, programming, threads, java, s3
editor: markdown
dateCreated: 2022-04-11T14:03:17.171Z
---

I don't really know how asynchronous and synchronous computation works, so I wanted to get that out of the way first. Before we test some things we need to know exactly what we're dealing with. When you execute something synchronously, it means that it finishes the execution before moving to something else. By executing something asynchronously, you can go on to the next one without having to wait for the execution to finish. It's like multitasking.

That being said, in terms of programming, asynchronous computation allows you to offload work. This means you can run more processes without affecting the main process/thread.
<br />

Synchronous means that there is one thread that serves everything in order. It can't do more than one thing at the same time, like scrolling through a list and listening to music in the application.

But, why do I want to use it asynchronously?Well, Let's take this for example: Take a generic web-app that fetches profile pictures, a forum and personal data on a single page. With a REST API, these most likely multiple different endpoints. So instead of fetching these endpoints separately, do it asynchronous. We can use the term time-slicing; the application could do multiple things simultaneously.
<br />

Okay, so I said before that future.get() waits for the current thread while simultaneously executing others, right? Now, how does that work exactly?
<br />

To demonstrate that, I've created a Unit-test that simulates asynchronous thread execution.

```java
class MediaListRepoTest {
    @Test
    void testFuture() throws ExecutionException, InterruptedException {
        //Thread testing
        String[] bruh = {"bruh", "another-bruh", "third-bruh"};
        ExecutorService executorService = Executors.newSingleThreadExecutor();
        System.out.println("Downloading more RAM");
        Future<String> testFuture = executorService.submit(new Callable<String>(){

            @Override
            public String call() throws Exception {
                for (int i = 0; i < 6; i++) {
                    Thread.sleep(1000);
                    System.out.println("bruh nap");
                }
                return bruh[1];
            }
        });
        System.out.println("Hacking Mittens..");
        Thread.sleep(2000);
        System.out.println("Videos found!");
        var bruh2 = testFuture.get();
        System.out.println(bruh2);
    }
}
```
To get briefly over it:

executorService creates an Executor that uses a single worker thread operating off an unbounded queue. Then, I use Future, I assume we know what future means, but we'll repeat to be sure: A Future represents the result of an asynchronous computation. Methods are provided to check if the computation is complete, to wait for its completion, and to retrieve the result of the computation). Nice.
I use Future to compute a string-type result. In this case, I print out "bruh nap" 6 times with a second interval. Notice how I have several more print-lines in the test. These are used to show simultaneous execution in the output.

As you can see, It will will execute print-lines simultaneously. You can notice with the "Videos found!" between the "bruh naps."

![testresult.png](/s3/portfolio/testresult.png)

Sweet! :3