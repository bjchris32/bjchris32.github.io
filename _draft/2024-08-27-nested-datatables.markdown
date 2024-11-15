---
layout: post
title:  "Implement nested datatables"
date:   2024-08-27 11:40:34 -0500
categories: rails
---

Some questions raised when implementing nested data tables.

## Questions
* In client side, can I use the js function in server side?
* In server side, can I use the js function in client side?

* In first erb page(server side), can I fetch the element in the second response(js.erb)?

## Errors after moving to server side rendering
* row is not a function
* can not redefine datatable in server side rendering

## Sol
* When in the first page, define the DataTable with option
* When in the js response, fetch the DataTable without option
  * This is not redefining the DataTable -> confirm it with document

## Other topics to learn
* server side processing: https://datatables.net/manual/server-side


## reference resources:
* Initial search:
  * [Creating Dynamic Nested Tables](https://datatables.net/forums/discussion/60684/creating-dynamic-nested-tables)

* Sol: Client side
  * [Nested Tables](https://datatables.net/forums/discussion/42045/nested-tables)
  * use modal: editor
  * align child table to parent table
  * child table as an independent table

* Sol2: Server side
  * Because the table is a partial(server side)
