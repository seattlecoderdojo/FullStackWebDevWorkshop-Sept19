# Week 2: Members-only

**FIRST AND FOREMOST:** Let's go back to glitch.com and open the projects we were working on last week. If you missed last week, you can clone [my project from last week](https://glitch.com/edit/#!/shocking-emoji), by following the link, clicking on the "shocking-emoji" title in the upper left of the screen, and clicking the "Remix Project" button. You will get my  page, but you can go back to [last week's write-up](../week1/readme.md) and learn how to customize it and make it your own.



What we're going to do this week:

1. Learn about node and its module system
2. Create our member page
4. Learn about sessions 
4. Keep someone out! 
5. Let them in!
6. Add a database
7. Add a login
8. Manage members



## What is Node.js

JavaScript started life way back in the 1990s as a language that let you make web pages do more programmatic things. It has NOTHING to do with Java. In fact, many people say that Java and JavaScript share as much in common as ham and hamsters.

![hamster](images/ham-ster.png)

We could go into the history of JavaScript and Node, but we came here to make stuff. History lessons are for the school part of the week. Let's just say it's JavaScript for controlling stuff on your web server.

## Node Modules

There are two main reasons Node caught on. 

One is that people felt it performed better than Apache, the most popular web server of the time. We can go into why people thought that, but again, we're not here for a history lesson. 

The second is node had just a medium selection of core functions, and then you just added modules to outfit a Node server with what you needed. Those modules are declared in your `package,json` file. Let's look at that file in our projects.

![cap of package.json](images/package1.jpg)

This file is standard for Node.js apps, tells you a lot about the app, and helps install the app on a server. It's in a format called JSON (pronounced like the name Jason), which means JavaScript Object Notation. Hopefully you know what an object is. But a very quick description is that it's a way of putting information and functionality into a package. 

The information is called properties. The functionality is called methods.

So an address object might have information like the address of someone's house and a property would be the name of the street they live on. A method might be a bit of code that redirects the user to a Google Maps page with the house marked on it.

An object will be wrapped in curly braces {}. We can see the whole thing is wrapped in curly braces. It's one big object. But inside, there are other sections wrapped in curly braces. Objects can have objects inside them... sort of like those Russian nesting dolls that fit inside each other.

![nesting dolls](images/matrioshka-1631194_640.jpg)

We'll get into methods later. We'll have to. But for now, let's look at properties. A property is the property name (usually in quotes), then a colon, then a value.

```javascript
"name": "hello-sqlite"
```

It's like a string, but because it's a property, we have to define it a little more formally.

Some of the properties have an object as their value. For example:

```javascript
  "dependencies": {
    "express": "^4.16.3",
    "sqlite3": "^4.0.0"
  }
```

The `dependencies` object tells us what modules our Node.js project is using. There are some core ones for reading files and doing basic things and they're included with Node, but for more extensive stuff, we load modules from a module store.

So if we're going to need more modules, we need to add them to our dependencies. For this project we'll add a few. But first let's just add one. Let's change that `dependencies` object.

Each module is declared as a property name that is the name of the module (it has to match the name in a package manager like [npmjs.org]()), then the value is the version. We'll get into why you might use the up arrow before it in a different class.

Remember to make sure that every property in the object except the last has a comma after it.

```javascript
  "dependencies": {
    "express": "^4.16.3",
    "sqlite3": "^4.0.0",
    "sequelise": "^5.18.4"
  }
```

Did you make the change?

HA! Tricked you! I broke your `package.json` file... sort of.

I did it for a good reason. If you ever learn anything about programming, learn this... Even for the best programmers, a lot of time is spent figuring out why the code they wrote doesn't work.

So if you're going to learn to program, you need to learn to fix your code.

With Node, the best place to start is the logs. 

In the lower left of your Glitch screen, click "Tools," then from the tools panel, click "Logs."

![tools screencap](images/tools1.jpg)

![screencap of log](images/logs1.jpg)

And there we see, you have a 404 or "not found" error for the `sequelise` module. There is no such module.

But the app is listening. It is running. Why? Because there's no code in our app that needs that module yet. If we had code in the app that needed it, that code would break and then the app might not run at all or might fail when we didn't expect it.

Who knows why it can't find `sequelise`? Because we spelled it wrong. That last s, should be a z. Let's fix it.

```javascript
  "dependencies": {
    "express": "^4.16.3",
    "sqlite3": "^4.0.0",
    "sequelize": "^5.18.4"
  }
```

What does the log say?

![screencap of log](images/logs2.jpg)

It not only found `sequelize`, but it installed it since it's seeing it for the first time. Now that module is available to your Node code and you debugged something. High five yourself.

Now let's add the other modules this app will need. 

We've got `express` which is the module working as the web server. We'll add `express-session` to help us remember information about the user without having to put it where other people can see it. 

`sqlite` is the module to give us a database for some of the fun stuff we'll be adding. `sequelize` is a module that makes using `sqlite` easier.

We'll add `body-parser` to make getting information submitted from web forms easier. And we'll add `bcrypt` because it provides encryption functions we'll use to help make everything more secure.

```javascript
  "dependencies": {
    "express": "^4.16.3",
    "sqlite3": "^4.0.0",
    "sequelize": "^5.18.4",
    "express-session": "^1.16.2",
    "body-parser": "^1.19.0",
    "bcrypt": "^3.0.6"
  }
```



