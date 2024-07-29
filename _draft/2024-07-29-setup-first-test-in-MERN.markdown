---
layout: post
title:  "MERN stack project - design the first model"
date:   2024-07-29 11:40:34 -0500
categories: MERN fullstack
---
This is a tutorial about MERN stack setup.

{% highlight javascript %}
{% endhighlight %}

I am designing a database schema for habit object to record the logs.

## test set up
* install necessary packages for jest in typescript

## data schema design
* What is the relationships between habit and its logs?
  * Compare the relationships
    * one-to-many
      * parent document stores the ids of children document in the array field
    * one-to-squillions
      * do not need to implement the ids in the parent. Make the parent id in the child instead.
  It is possible to that a users would have multi-million records. But, the habit should keep in the database for up to 10000 years. It would be an overkill to use one-to-squillions. As a result, we use one-to-many to explain the relationship between habit and logs.



## Take away:
  * Takeaway from the rules of thumb in MongoDB design
  > * Embed the N side if the cardinality is one-to-few and there is no need to access the embedded object outside the context of the parent object.
  > * Use an array of references to the N-side objects if the cardinality is one-to-many or if the N-side objects should stand alone for any reasons.
  > * Use a reference to the One-side in the N-side objects if the cardinality is one-to-squillions.


## reference resources:

[MongoDB schema best practice]: https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design
