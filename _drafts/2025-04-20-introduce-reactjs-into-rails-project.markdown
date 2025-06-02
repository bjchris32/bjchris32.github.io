---
layout: post
title:  "Introduce ReactJS into Rails 5.2 project using webpacker"
date:   2025-04-20
tags: [rails, reactJS]
img: posts/ruby-on-rails.webp
read_time: true
show_date: true
---

In this post, I will share my experience and the problems I solved while introducing ReactJS to the Rails 5.2 project as well as deploying onto production server. Since Rails version 5.2, we could use Webpacker to install more modern js modules instead of using the default Sprocket. However, it is not saying we will completely deprecate Sprocket. Instead, Sprocket and Webpacker can run in parallel.

## Problems solved on development environment

- Error in `babel.config.js`
  ```
  ERROR in ./app/javascript/packs/application.js
  Module build failed (from ./node_modules/babel-loader/lib/index.js):
  Error: Cannot find package '@babel/plugin-proposal-private-methods' imported from /Users/bshao/projects/deput/babel-virtual-resolve-base.js

  ```
  - solution: some dependent [library name changed](https://github.com/rails/rails/issues/48372) after the `react-rails` gem was released. We need to manually change the libray name in `babel.config.js`. If the error persists and show as below:

  ```
  Uncaught Error: Module build failed (from ./node_modules/babel-loader/lib/index.js):
  Error: Cannot find package '@babel/plugin-proposal-private-methods' imported from /Users/bshao/projects/deput/babel-virtual-resolve-base.js
  ```

  Try to stop the webpacker server and clean the webpacker cache after modification:
  ```
  rm -rf tmp/cache
  ```


- Error when using `react-rails`
  - error logs in `application.js`:

  ```
  import ReactRailsUJS from 'react_ujs';
  ReactRailsUJS.useContext(require.context('components', true));
  ```

  - [solution](https://github.com/reactjs/react-rails/issues/721): `yarn add react_ujs`

## Problems solved on production environment

- Errors met when `yarn install`. There is connection error when I tried to execute `yarn install`. I also found `curl -I https://registry.yarnpkg.com` has a connection error: `curl: (35) Recv failure: Connection reset by peer`
  - Since there is another source that I could install the packages. I decided to switch registry to npm registry.
  ```
  yarn config set registry https://registry.npmjs.org
  yarn cache clean
  yarn install
  ```

## How to deploy?
  * `RAILS_ENV=production bundle install`: install the webpacker and the react-rails gems.
  * `yarn install --production`: install the js modules and put into `node_modules` directory.
  * `RAILS_ENV=production bundle exec rails webpacker:clobber`: clean the previously precompiled assets to prevent from accumulating unused assets
  * `RAILS_ENV=production bundle exec rails webpacker:compile`: precompile new asset. Then, we could now savely remove the `node_modules` directory to save the storage space on server.

