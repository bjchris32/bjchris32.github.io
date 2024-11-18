---
layout: post
title:  "Change Jekyll Theme without forking the theme repository"
date: 2024-11-17 11:40:34 -0500
tags: [Writing]
img: posts/tech-writing.webp
read_time: true
show_date: true
---

## Context:
Originally, I have a jekyll with default theme. But, in this theme, I can not categorize the blog posts. So, I want to change the theme to support categories.

I found a [template](https://github.com/the-mvm/the-mvm.github.io) that looks good to me. Problem is most of the themes mentioned that we need to fork their repository and copy-paste all of the posts. However, I don't want to fork the new theme repository. Instead, I want to reuse my original repository.

I found a [SO](https://stackoverflow.com/questions/31327045/switch-theme-in-an-existing-jekyll-installation).
I followed the instruction to create a new branch:
```
git checkout --orphan newtheme
git rm -rf .
git clean -dfx
```
Then, set the upstream to the new repository to pull the code into the new branch in local.
```
git remote add upstream https://github.com/the-mvm/the-mvm.github.io.git
git fetch upstream
git pull upstream main
```

After pulling the code from theme template, I will copy the files in my `posts` and `drafts` folder from `main` branch.
```
git checkout main -- _posts
git checkout main -- _drafts
git checkout main -- CNAME
```

## Problem:
When merging the main with newtheme:
`git merge -s ours main`
I met an error: `fatal: refusing to merge unrelated histories`.

## Solution:
The reason is that I opened a completely new branch without any shared commits.
I solved this issue by merging the `main` branch into `newtheme` and resolve all of the conflicts.
```
git checkout newtheme
git merge main
```

At last,
```
git checkout main
git merge newtheme
```


## Reference
* https://stackoverflow.com/questions/31327045/switch-theme-in-an-existing-jekyll-installation
* https://github.com/the-mvm/the-mvm.github.io
