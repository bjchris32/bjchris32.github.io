---
layout: post
title:  "MERN project setup: setup Nodejs server and Typescript"
date:   2024-07-19 11:40:34 -0500
tags: [MERN, Fullstack, Backend, NodeJS, Typescript, MongoDB, Docker]
img: posts/tech-writing.webp
read_time: true
show_date: true
---
This is a tutorial about MERN stack setup. Through this article, we could understand the directory structure of MERN project, how to setup backend environments. In next article, I will detail more about how to set up frontend and how to dockerize each services including database.

## Outlines
* Initialize server and client directories in MERN directory
* Install NodeJS packages in server directory
* Spin up MongoDB docker container and connect the container


## Directories structure
Firstly, we could just make two directories `client` and `server` in the project root directory, which is usually the directory where the `README.md` exists.
```
mern-project/
├── client/
├── server/
└── README.md
```

## Install Backend Packages
In `server` directory, use command `npm init -y` to create `package.json`.
After generating `package.json`, add necessary packages to make the MERN project spin up with database.

* Typescript: it is just a tool to transpile ts to js. In this way, we could detect Javascript error in early development stage. We do not need it when everything is built and ready for production. Hence, just install Typescript in dev environment!
{% highlight shell %}
npm i -D typescript @types/express @types/node
{% endhighlight %}

* nodemon: enhance live transpile in Typescript
{% highlight shell %}
npm i -D nodemon ts-node
{% endhighlight %}

* mongoose: a library
{% highlight shell %}
npm install dotenv express mongoose        # Install the main packages
{% endhighlight %}

* Other dependencies: since node and express still do not support Typescript at the time of writing. We will need to install additional packages to support Typescript transpile.
{% highlight shell %}
npm install -D @types/node @types/express  # Install types for Node and Express
{% endhighlight %}

After installing the packages, modify the scripts in `package.json`:
{% highlight json %}
"scripts": {
  "build": "npx tsc",
  "start": "node dist/index.js",
  "dev": "nodemon src/index.ts",
}
{% endhighlight %}

In this way, we could specify the folder to watch and proper file extension to transpile after saving.
{% highlight shell %}
npm run dev
{% endhighlight %}

## MongoDB connection
* Use Docker to spin up a MongoDB container.
{% highlight shell %}
docker run --name mongodb -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password mongo
{% endhighlight %}

* Connect MongoDB through mongosh in command line.
{% highlight shell %}
mongosh mongodb://mongodb:27017/mydatabase
{% endhighlight %}

* Connect through mongoose in NodeJS
In the file `server/src/index.ts`, add the following script to test it out.
{% highlight javascript %}
import mongoose from 'mongoose';
const mongoURI = process.env.MONGO_URI || 'mongodb://mongodb:27017/mydatabase';
mongoose.connect(mongoURI).then(() => {
  console.log('Connected to MongoDB');
}).catch((err: any) => {
  console.error('Failed to connect to MongoDB', err);
});
{% endhighlight %}

We will see the log in the console saying `Connected to MongoDB`.

## Reference resources:
[MERN setup](https://blog.logrocket.com/how-to-set-up-node-typescript-express/)
