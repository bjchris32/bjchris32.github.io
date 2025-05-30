---
layout: post
title:  "Advantages of using ReactJS in Rails project"
date:   2025-05-29
tags: [rails, reactJS]
img: posts/ruby-on-rails.webp
read_time: true
show_date: true
---

## Foreword

Recently, I have been working on a feature to display a list of file records stored in various data repositories. The goal is to present different data repositories along with their corresponding file records on a single page. The user interface consists of a tab widget for switching between data repositories, and within each tab's content, there is a table widget listing all the file records.

It's important to note that a file record can also represent a folder. When a user clicks on a folder record in the table, the table content needs to be refreshed. To avoid loading all file records at once (which could lead to performance issues), we aim to update the table content partially and display only the file records in the current path.

I intend to use this feature as an example to showcase the benefits of using ReactJS over traditional Ajax/JQuery in terms of DOM manipulation, component isolation, and maintainability.

Let's delve into the code to see these advantages in action.

## Implementation

### Ajax/JQuery Implementation
<div style="max-height: 600px; overflow: auto; border: 1px solid #ccc;">
  <script src="https://gist.github.com/bjchris32/e493a3819fef9b55d00dd7cceee67a50.js"></script>
</div>

* We need to know there would be some events that will trigger partial loading. As indicated in [line 29 - line 51](https://gist.github.com/bjchris32/e493a3819fef9b55d00dd7cceee67a50#file-catalog-html-erb-L29-L51)
  * Initial loading
  * Switching tabs
  * Switching directories

-> Need to call the loading function three times.


* Imperative DOM manipulation -> we tell the browser *how* to do things step by step - check the state, change the DOM manually.
  * For example, in [line 71 - line 102](https://gist.github.com/bjchris32/e493a3819fef9b55d00dd7cceee67a50#file-catalog-html-erb-L71-L102)
    * declare a table
	  * add one row after another
	  * append the table
* There is only one global scope. Any function could manipulate any DOM node by class or id. However, this could easily lead to conflicts.
  * For example, there would be more than one tab widget in one page. Two event handlers for switching the tab will need to use different id as query condition to locate the tab widget.



### ReactJS Implementation
<div style="max-height: 700px; overflow: auto; border: 1px solid #ccc;">
  <script src="https://gist.github.com/bjchris32/024528bc89e3d59abbe30100e18bad49.js"></script>
</div>

* Every component can have [some states](https://react.dev/learn/managing-state) as in [line 6 - line 7](https://gist.github.com/bjchris32/024528bc89e3d59abbe30100e18bad49#file-catalog-jsx-L6-L7)
* Built in callback [useEffect](https://react.dev/learn/synchronizing-with-effects) as in [line 9 - line 20](https://gist.github.com/bjchris32/024528bc89e3d59abbe30100e18bad49#file-catalog-jsx-L9-L20)
  * The ReactJS engine monitors the state to execute the callback function autonomously -> No need to manually hook up event handlers multiple times.
* Declarative DOM manipulation
  * You describe what the UI should look like based on the current state.
  * Components are isolated and we do not need to query the DOM node.

## Conclusion

Using ReactJS offers several key advantages over traditional Ajax/jQuery:
* Declarative UI – Describe what to render instead of how to manipulate the DOM.
* Component Isolation – Encapsulated logic and state reduce side effects.
* Modularity – Reusable, self-contained components improve maintainability.
* State Management – Hooks like useState and useEffect simplify data flow.
* Automatic UI Sync – UI updates automatically when state changes.

That said, Ajax/jQuery still has its place. It’s lightweight, quick to set up, and perfectly suitable for small projects. However, as the project grows and user interactions become more complex, ReactJS becomes the top choice for scalability, maintainability, and long-term efficiency.
