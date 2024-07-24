---
layout: post
title:  "MERN stack project setup"
date:   2024-07-19 11:40:34 -0500
categories: MERN fullstack
---
This is a tutorial about MERN stack setup.

{% highlight javascript %}
{% endhighlight %}

## Motivation
* Learn typescript by doing project

## Workflows
* minimal server
* just install typescript in dev environment!
{% highlight shell %}
npm i -D typescript @types/express @types/node
{% endhighlight %}

* change js to ts

* enhance live transpile in typescript
{% highlight shell %}
npm i -D nodemon ts-node
{% endhighlight %}

* modify the script
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



* set up mongodb on docker and connect through mongoose
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

* dockerize server
docker build -t habicise_server .

* use network in docker-compose file to communicate

* dockerize client
  * do not need to use nginx in developmenet
  * separate dev and prod environment




## reference resources:

[MERN setup]: https://blog.logrocket.com/how-to-set-up-node-typescript-express/
