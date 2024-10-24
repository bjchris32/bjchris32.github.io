---
layout: post
title:  "MERN project setup: setup Nodejs server and Typescript"
date:   2024-07-19 11:40:34 -0500
categories: MERN fullstack
---
This is a tutorial about MERN stack setup. Through this project, we could understand the directory structure of MERN project and how to dockerize each services.


## Outlines
* Initialize server and client directories
* Dockerize the server, database and client services

### project directories overview

### Install development packages:
* typescript: it is just a tool to transpile ts to js. In this way, we could detect Javascript error in early development stage. We do not need it when everything is built and ready for production. Hence, just install Typescript in dev environment!
{% highlight shell %}
npm i -D typescript @types/express @types/node
{% endhighlight %}

* nodemon: enhance live transpile in Typescript
{% highlight shell %}
npm i -D nodemon ts-node
{% endhighlight %}

After installing the packages, modify the scripts in `package.json`:
{% highlight json %}
"scripts": {
  "build": "npx tsc",
  "start": "node dist/index.js",
  "dev": "nodemon src/index.ts",
}
{% endhighlight %}

  * specify the folder to watch and the file extension
    * transpile after saving
    {% highlight shell %}
    npm run dev
    {% endhighlight %}



### set up mongodb
Set up on docker and connect through mongoose.
  * need to create user in admin and test it with mongoosh
{% highlight shell %}
mongosh mongodb://mongodb:27017/mydatabase
{% endhighlight %}

  * connect through mongoose in nodejs
{% highlight javascript %}
const mongoURI = process.env.MONGO_URI || 'mongodb://mongodb:27017/mydatabase';
mongoose.connect(mongoURI).then(() => {
  console.log('Connected to MongoDB');
}).catch((err: any) => {
  console.error('Failed to connect to MongoDB', err);
});
{% endhighlight %}

### Dockerize services
* dockerize MongoDB
* dockerize server
{% highlight shell %}
docker build -t habicise_server .
{% endhighlight %}

* dockerize client
  * do not need to use nginx in developmenet
  * separate dev and prod environment

* How do client and server services communicate?
  * use network in docker-compose file to communicate

## Reference resources:
[MERN setup](https://blog.logrocket.com/how-to-set-up-node-typescript-express/)
