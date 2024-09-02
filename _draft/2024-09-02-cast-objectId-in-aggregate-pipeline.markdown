---
layout: post
title:  "Cast ObjectId in aggregate match"
date:   2024-08-27 11:40:34 -0500
categories: mongoosh, mongoDB
---

## Problem:
I can find the documents only with string: `const commit = await Commit.findById(req.params.id);`
However, I can not find the documents with just string:
```
    const commitsByDate = await Commit.aggregate([
      { $match : { habit: req.params.id } },
      {
        $group: {
          _id: {
            $dateToString: { format: '%Y-%m-%d', date: '$createdAt' },

          },
          count: { $sum: 1 },
        },
      },
      {
        $sort: { _id: 1 }, // Sort by date for consistency in results
      },
    ]);
```

## Solution:
Cast the objectId:
```
    const commitsByDate = await Commit.aggregate([
      { $match : { habit: new mongoose.Types.ObjectId(req.params.id) } },
      {
        $group: {
          _id: {
            $dateToString: { format: '%Y-%m-%d', date: '$createdAt' },

          },
          count: { $sum: 1 },
        },
      },
      {
        $sort: { _id: 1 }, // Sort by date for consistency in results
      },
    ]);
```

## Why is it?
TODO: check the documents



https://stackoverflow.com/a/28796576
