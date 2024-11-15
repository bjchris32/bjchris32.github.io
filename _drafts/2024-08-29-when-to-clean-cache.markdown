---
layout: post
title:  "docker compose options explained"
date:   2024-08-27 11:40:34 -0500
categories: rails
---

## Context:
I am using docker compose in my MERN project.
After npm install, the application does not load the latest packages.

## Solution:
I used `docker compose up --force-recreate --no-deps` to load all of the packages.
But, I still need to figure out the reason why I need to recreate when it is live compiling in my development mode.


## Reference
* https://stackoverflow.com/questions/36884991/how-to-rebuild-docker-container-in-docker-compose-yml