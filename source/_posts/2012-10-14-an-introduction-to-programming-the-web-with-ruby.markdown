---
layout: post
title: "A Brief Overview of Programming the Web with Ruby"
date: 2012-10-14 18:39
comments: true
categories:
---

Programming for the web is limited only by the person or persons behind the keyboard. Programming for the web with Ruby has an elegance and positive energy which pulls me in. I recently came across a great Speaker Deck slide from ['RailsGirls Ukraine'](https://github.com/rgua) which I will use to explain a brief overview of programming for the web using Ruby.

<div class='speakerdeck center' style='width: 400px;'>
<script async class="speakerdeck-embed" data-id="50701165dbcbfb00020788d6" data-ratio="1.3333333333333333" src="//speakerdeck.com/assets/embed.js"></script>
</div>

## Computers Are Dumb

<div class='speakerdeck right' style='width: 200px;'>
<script async class="speakerdeck-embed" data-slide="2" data-id="50701165dbcbfb00020788d6" data-ratio="1.3333333333333333" src="//speakerdeck.com/assets/embed.js"></script>
</div>
<div class='speakerdeck right' style='width: 200px;'>
<script async class="speakerdeck-embed" data-slide="3" data-id="50701165dbcbfb00020788d6" data-ratio="1.3333333333333333" src="//speakerdeck.com/assets/embed.js"></script>
</div>

Contrary to popular belief, computers are stupid. They do exactly what you tell them to do. If I tell you to make me a grilled cheese sandwich, I can expect at a minimum a couple of slices of bread with melted cheese in the middle. If I request the same from a computer, I will get nothing. I have to tell the computer a series of hundreds of commands to explain every minute detail to get my sandwich.

Programming is telling a computer exactly what you want it to do.

## Doing it All with Ruby

The Ruby programming language was created in 1995 by Yukihiro Matsumoto (also known as 'Matz'). Matz created the Ruby language because he wanted to simply create programs in a language that made him happy. This thought process is reflective throughout the Ruby community. In fact there is a well know acronym within the Ruby community known as MINSWAN (Matz is nice so we are nice).

The Ruby language is desinged to emphasize human readability rather than machine readability. As reflected in the aforementioned Speaker Deck, take a look at the following code written in a C language followed by the same output written in Ruby.

{% codeblock holler.cpp %}
using namespace std;

int main ()
{
  cout << "Hello blog reader number 1!";
  return 0;

{% endcodeblock %}

and, now the Ruby version

{% codeblock holler.rb %}
puts "Hello blog reader number 1!"
{% endcodeblock %}

Seriously, Ruby is that much more awesomer!

## How the Web Works

<div class='speakerdeck center' style='width: 300px;'>
<script async class="speakerdeck-embed" data-slide="8" data-id="50701165dbcbfb00020788d6" data-ratio="1.3333333333333333" src="//speakerdeck.com/assets/embed.js"></script>
</div>

The internet is comprised of billions of unique IP addresses. Every machine, from your computer to your smartphone to the server that displays your favorite website, is communicating through this unique address.

It is nearly impossible for you to remember the IP address of any single website, let alone all of the websites you enjoy visiting. For this reason, we use Domain Name Servers (DNS) to assign each website to a human readable domain name.

## The Anatomy of a Website

Now that you know how we communicate with a website, the fun part begins! Most websites you visit are "Dynamic" in that they process data on the server side based on continuous input/output. These websites use applications, databases, and servers in order to offer up a multitude of content. Let's use the RailsGirls presentation to look a little deeper.

<div style="clear:both"></div>

<div class='speakerdeck right' style='width: 200px;'>
<script async class="speakerdeck-embed" data-slide="12" data-id="50701165dbcbfb00020788d6" data-ratio="1.3333333333333333" src="//speakerdeck.com/assets/embed.js"></script>
</div>

### The Client

On the web, the "Client" refers to the end user. In most cases, this is the web browser on your computer or smartphone. This browser is what we use to communicate with the Application, Database, and Web Server.

<div style="clear:both"></div>

### Application

<div class='speakerdeck right' style='width: 200px;'>
<script async class="speakerdeck-embed" data-slide="14" data-id="50701165dbcbfb00020788d6" data-ratio="1.3333333333333333" src="//speakerdeck.com/assets/embed.js"></script>
</div>

The application is the brains behind any website. While all components of a website rely on each other equally, the application is the center, the leader, the guy everyone else in the stack follows. This is where the Ruby programming language comes into play. You can see on the slide to the right that there are many possible languages written for the web. Although Ruby is certainly not the only language to program for the web, I love Ruby and you should too!

<div style="clear:both"></div>

### Database

<div class='speakerdeck right' style='width: 200px;'>
<script async class="speakerdeck-embed" data-slide="15" data-id="50701165dbcbfb00020788d6" data-ratio="1.3333333333333333" src="//speakerdeck.com/assets/embed.js"></script>
</div>

The database is where all of the information on a website or web application is stored. How do you think Instagram keeps track of all of the awesome pictures you've taken lately? The application communicates with the database everytime you login, accesses all of your information, and serves it to you (the client). See, it all makes sense now!

<div style="clear:both"></div>

### Web Server

<div class='speakerdeck right' style='width: 200px;'>
<script async class="speakerdeck-embed" data-slide="16" data-id="50701165dbcbfb00020788d6" data-ratio="1.3333333333333333" src="//speakerdeck.com/assets/embed.js"></script>
</div>

As we learned earlier, the web server is how where all communication on the web happens. Think of the web server as a highway with a ton of roads (and no speeding tickets!). There are several types of servers but they all share a similar purpose, COMMUNICATION.

<div style="clear:both"></div>

So, there you have it. A very basic overview of how the internets work. This is my first post, things will get a bit more complicated from here!

Thanks to RailsGirls Ukraine for putting together this awesome visual for me to use!