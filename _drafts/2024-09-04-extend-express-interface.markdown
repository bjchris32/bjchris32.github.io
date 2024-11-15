---
layout: post
title:  "extend express interface"
date:   2024-08-27 11:40:34 -0500
categories: rails
---

## Context:
I want to assign the user property in express request after authentication.

## Solution:
Extend the original request interface as followed.
```
declare global {
  namespace Express {
    interface Request {
        ...
```

## Reference
* https://stackoverflow.com/questions/37377731/extend-express-request-object-using-typescript
* https://basarat.gitbook.io/typescript/type-system/lib.d.ts

