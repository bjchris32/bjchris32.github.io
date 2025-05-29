---
layout: post
title:  "Advantages of using ReactJS in Rails project"
date:   2025-05-29
tags: [rails, reactJS]
img: posts/ruby-on-rails.webp
read_time: true
show_date: true
---

Recently, I am implementing a feature to show a list of file records which stored in different data repositories. I would like to show different data repositories as well as its related file records in the same page. The user interface is a tab widget to switch the data repositories and in the tab content, there would be a table widget to list all of the file records.

One thing to notice is that a file record could also be a folder, we will need to refresh the table content whenever the user click on the folder record in the table. To prevent from loading all of the the file records in one shot(recursion), we will need to partially update the table content and only show the file records in current path.

I want to use this example feature to demonstrate the advantages of using ReactJS instead of Ordinary Ajax/JQuery in terms of DOM Manipulation, Component Reusability, and Maintainability.

Let’s take a look a the code directly.

### Ajax/JQuery Implementation
<div style="max-height: 600px; overflow: auto; border: 1px solid #ccc;">
  <script src="https://gist.github.com/bjchris32/e493a3819fef9b55d00dd7cceee67a50.js"></script>
</div>

* We need to know there would be some events that will trigger partial loading. As indicated in [line 29 - line 51](https://gist.github.com/bjchris32/e493a3819fef9b55d00dd7cceee67a50#file-catalog-html-erb-L29-L51)
  * Initial loading
  * Switching tabs
  * Switching directories

-> Need to call the loading function three times.


* Imperative DOM manipulation -> tell the browser *how* to do things step by step - check the state, change the DOM manually.
  * the html tags are spread across the function: For example, in [line 71 - line 102](https://gist.github.com/bjchris32/e493a3819fef9b55d00dd7cceee67a50#file-catalog-html-erb-L71-L102)
    * declare a table
	* add one row after another
	* append the table
* There is only one global scope. Any function could manipulate any DOM element with the specific jquery. -> id or class name may conflict and lead to wrong query.
  * For example, there would be more than one tab widget in one page. Event handler for switching the tab will need to use id as query condition to locate the tab widget.



### ReactJS Implementation
<div style="max-height: 700px; overflow: auto; border: 1px solid #ccc;">
  <script src="https://gist.github.com/bjchris32/024528bc89e3d59abbe30100e18bad49.js"></script>
</div>

* Every component can have [some states](https://react.dev/learn/managing-state) as in [line 6 - line 7](https://gist.github.com/bjchris32/024528bc89e3d59abbe30100e18bad49#file-catalog-jsx-L6-L7)
* Built in callback [useEffect](https://react.dev/learn/synchronizing-with-effects) as in [line 9 - line 20](https://gist.github.com/bjchris32/024528bc89e3d59abbe30100e18bad49#file-catalog-jsx-L9-L20)
  * The ReactJS engine monitors the state to execute the callback function autonomously
    * no need to register the partial loading multiple times
* Declarative DOM manipulation
  * do not need to query the DOM -> JS behavior is described around the UI(html tags)