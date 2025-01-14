---
layout: post
title:  "MERN project setup: setup Nodejs server and Typescript"
date:   2024-07-19 11:40:34 -0500
categories: MERN fullstack
---
This is a tutorial about MERN stack setup. Through this article, we could understand the directory structure of MERN project, how to setup frontend and backend environments, and how to dockerize each services including database.

## Outlines
* Initialize server and client directories in MERN directory
* Install NodeJS packages in client and server
* Dockerize the database, server and client services

### Directories structure
Firstly, we could just make two directories `client` and `server` in the project root directory, which is usually the directory where the `README.md` exists.
```
mern-project/
├── client/
├── server/
└── README.md
```

### Install Packages
#### Backend packages
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

#### MongoDB connection
We could use Docker to spin up a MongoDB.
{% highlight shell %}
docker run --name mongodb -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password mongo
{% endhighlight %}
This command will start a MongoDB container with the username `admin` and password `password`. You can then connect to this MongoDB instance using mongoose in your Node.js application.

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
