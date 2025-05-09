### Introduction

NodeJS (or just 'Node') has been steadily gaining popularity since its creation in 2009. The internet is flooded with courses and articles about it, installing it is a prerequisite for pretty much any front-end development work, and of course the amount of jobs that require knowledge of it are also on the rise.

### Lesson overview

This section contains a general overview of topics that you will learn in this lesson.

- Describe the purpose of a server.
- Describe the differences between static and dynamic sites.
- Explain why you might need a back-end for your project.
- Explain when you wouldn't need a back-end for a project.
- Explain the event loop.
- Understand the origin of the Node.js runtime.
- Write a basic "hello world" application and run it in the console of your machine.
- Understand what Node.js really is.

### What is Node?

The [Node.js website](https://nodejs.org/en/about/) declares:

> As an asynchronous event driven JavaScript runtime, Node is designed to build scalable network applications.

This is a definition that requires a little unpacking.

The important bit to understand right up front is that Node is a "JavaScript runtime". When JavaScript was first created, it was designed to run *in the browser*. This means that it was impossible to use JavaScript to write any kind of program that was not a website. Node brings JavaScript *out* of browser-land. This allows developers to use JavaScript to accomplish pretty much anything that other popular server-side languages such as Ruby, PHP, C# and Python can do. So, at its most basic level, Node allows you to run JavaScript code on a machine such as your local computer or a server without having to go through a web browser.

To facilitate this, Node has some added functionality that is not found in browser-based JavaScript, such as the ability to read and write local files, create http connections and listen to network requests.

### Event driven

Back to the definition from Node's website: Node is an **asynchronous event driven** JavaScript runtime. In this context **asynchronous** means that when you write your code you do not try to predict the exact sequence in which every line will run. Instead you write your code as a collection of smaller functions that get called in response to specific events such as a network request (**event driven**).

For example, let's say you are writing a program and you need it to do the following. It should read some text from a file, print that text to the console, query a database for a list of users and filter the users based on their age.

Instead of telling your code to do those steps sequentially like so:

1. Read File
1. Print File Contents
1. Query Database
1. Filter Database Query results

You can break up the task like so:

1. Read File *AND THEN* Print File Contents
1. Query Database *AND THEN* Filter Database Query Results.

When you run this program Node will start at the top and begin reading the file but since that is an action that takes some time it will immediately begin running the second step (querying the database) while it's waiting on the file to finish reading.

While both of these processes are running, Node sits and waits on an *event*. In this case, it is waiting on the completion of both processes, the reading of a file and the database query. When either of these tasks are finished, Node will fire off an event that will run the next function we've defined. So if the read-file process finishes first, it will print the file contents. If the database query finishes first, it will start the filtering process. As the programmer, we don't know or care which order the two processes are going to be completed. If this code was processed synchronously (rather than asynchronously) we would have to wait for each step in the program before moving on to the next one, which could cause things to slow down considerably. If the file that we needed to read was really long then we might have to wait a few seconds before the database query could begin.

This process is almost exactly like the way that you would use `addEventListener` in front-end JavaScript to wait for a user action such as a mouse-click or keyboard press. The main difference is that the events are going to be things such as network requests and database queries. This functionality is facilitated through the use of callbacks. Callbacks are incredibly important to Node, so take a minute to read through this [article about understanding callbacks](https://dev.to/i3uckwheat/understanding-callbacks-2o9e) to make sure you're up to speed.

Let's look at a quick real-world example:

```javascript
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  res.end('Hello World!');
}).listen(8080);
```

This snippet is from the very first lesson in a tutorial that you'll be following very soon. Basically this code is creating a server and saying, "any time we get a network request, run this callback function". This function happens to respond with the text 'Hello World!'. So if you go to a browser and navigate to the correct address and port, you would see that text on your screen.

<div class="lesson-note" markdown="1">

#### Using React in the Node.js course

We will start by focusing on server-side concepts, so client-side things like React will be left for later when you start combining more complex frontends and backends together. You should follow the course as it is written; deviating from the directions can make it more difficult than it needs to be.

</div>

### Assignment

<div class="lesson-content__panel" markdown="1">

1. This [short module on "The Server Side" from MDN](https://developer.mozilla.org/en-US/docs/Learn/Server-side/First_steps) is a great source for the background knowledge you need. Read through at least the first two articles posted under the 'Tutorials' section: Introduction to the server side and Client-Server Overview. The other two are interesting and worth reviewing, but less relevant to our immediate concerns.
1. To gain a little more insight into the nature of Node, and to unpack the rest of the above definition, read this [article about NodeJS](https://medium.freecodecamp.org/what-exactly-is-node-js-ae36e97449f5).
1. What is the Node Event Loop? You may remember about this long, but *really* [fantastic video about event loops](https://www.youtube.com/watch?v=8aGhZQkoFbQ) from an earlier part of the course... don't skip it!
1. Take a few minutes to go through the "Getting Started" section of the new official [Node.js website](https://nodejs.org/en/learn/getting-started/introduction-to-nodejs). Read up until, but not including, the TypeScript module.
1. This [short video about NodeJS](https://www.youtube.com/watch?v=uVwtVBpw7RQ) is a great introduction as well!

</div>

### Knowledge check

The following questions are an opportunity to reflect on key topics in this lesson. If you can't answer a question, click on it to review the material, but keep in mind you are not expected to memorize or master this knowledge.

- [What is Node?](#what-is-node)

### Additional resources

This section contains helpful links to related content. It isn't required, so consider it supplemental.

- Read this article on [7 awesome things you can build with Node.js](https://blog.teamtreehouse.com/7-awesome-things-can-build-node-js).
