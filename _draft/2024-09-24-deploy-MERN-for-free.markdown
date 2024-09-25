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
further study: explain the property `sameSite` and `secure`.
refer to: https://andrewlock.net/understanding-samesite-cookies/

## Yet another problem
I tested on my iphone with safari. The user will automatically log out after refreshing the browser, which means the token is not persistent.

## Ultamate Solution:
Use the same root domain in both hosts on netlify and render.
Okay, I know it is not completely free.
When we set the subdomain on netlify and render, they will share the same root domain.
At last, the `sameSite` could be set to `strict`.
The token will be persistent and the user could maintain the login status.
What made me impressed is both netlify and render handle the https certificate for me.

TODO: further study
Why I need to create NS record for netlify server, but only CName record for render server?
What is the difference between NS record and CName?

## Reference
* https://docs.netlify.com/domains-https/netlify-dns/#add-a-domain
* https://docs.netlify.com/domains-https/custom-domains/configure-external-dns/#configure-a-subdomain
* https://docs.render.com/custom-domains#2-configure-dns-with-your-provider
* https://docs.render.com/configure-other-dns#configuring-www-and-other-subdomains
