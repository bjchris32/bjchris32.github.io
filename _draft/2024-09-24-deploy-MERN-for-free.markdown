---
layout: post
title:  "deploy MERN side project on completely free hosts"
date:   2024-08-27 11:40:34 -0500
categories: MERN, netlify, render
---

## Context:
I want free service


## Problem:
```
In MERN project, I deployed the client in netlify and the server in render.
In local host, it works. However, I found an issue that the token in the cookie will disappear after I refresh the page in the browser. For example, the user login and the server will set the token in the cookie. However, after refresh the token, the token in the cookie is gone. Why? How to resolve it?
```

## Solution:
Set cookie property `SameSite` to `none`.
This is because I hosted my client and server service on different hosts.
TODO: explain the property `sameSite` and `secure`.






## Reference
* https://www.reddit.com/r/typescript/comments/98siz7/typescript_file_naming_conventions/
* https://stackoverflow.com/questions/43973199/file-naming-conventions-in-reactjs
* https://github.com/airbnb/javascript/tree/master/react