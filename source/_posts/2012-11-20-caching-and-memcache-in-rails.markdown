---
layout: post
title: "Caching and Memcached in Rails"
date: 2012-11-20 10:45
comments: true
categories: 
published: false
---

##Sweepers

Sweeping is a mechanism which allows you to get around having a ton of ''''expire''' calls in your code. It does this by moving all the work required to expire ahed contnet into a ActionCongroller::Caching::Sweeper subclass.

##SQL Caching

You can also cache the results from each SWL query Rails encounters so then next request will use the cached result instead of running a query against the database.

##Memcached

Memcached allows you to take memory from parts of your system where you have more than you need and make it accessible to areas where you have less than you need. Memcached is an in-memery key-value store for small chuncks of arbitrary data, such as strings or objects, which come in as results of database calls, API calls, or page rendering.