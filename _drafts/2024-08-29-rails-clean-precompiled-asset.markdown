---
layout: post
title:  "Rails clean precompiled asset"
date:   2024-08-27
tags: [rails, issue solved]
img: posts/ruby-on-rails.webp
read_time: true
show_date: true
---

## Context:
I would like to live compile the assets on production.
But, newly added CSS is not applied to the production.
I found `config.assets.compile = false`, which means the production is using precompiled assets.
However, after setting, `config.assets.compile = true`, it is still not working.

## Solution:
* Clean the precompiled assets `RAILS_ENV=production rake assets:clean`
-> Still not working, because there is still `public/assets`

* Another command: `RAILS_ENV=production rake assets:clobber`
-> `public/assets` is removed. Now the assets are removed.
Live compile now.
Congrats!

## Questions:
* What is the difference between `RAILS_ENV=production rake assets:clean` and `RAILS_ENV=production rake assets:clobber`?
* clean -> only clean the old precompiled assets
* clobber -> clean all of the precompiled assets

## Reference
* live compile: https://guides.rubyonrails.org/asset_pipeline.html#live-compilation
