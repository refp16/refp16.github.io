---
layout: page
title: "Zeitz's ''The Art and Craft of Problem Solving'' -- Solved!"
description: ""
---
{% include JB/setup %}



##About##

<img src="/assets/images/artandcraftbook.png" alt="Book cover" width="250">

[Go to posts in this category](/about-cat-zeitzps.html#Posts-ref-zeitzps)

This category concerns posts documenting the thought process I go through
when problem-solving Paul Zeitz's _The art and Craft of 
Problem Solving_, Second Edition (c) John Wiley & Sons, Inc., 2007.
I find it intriguing, to say the least, how different people arrive at
the same solutions in such distinct ways. Here I share the paths I followed.

My goal is to post the answer to each problem using my own means only.
If I happen to solve the problem in a 
fashion similar to the book, I will still post it. Along with what I believe
are the correct answers, I will try to add my wrongful lines of thinking 
just to show that problem solving is not as straightforward and ordered as 
some readings suggest. If I find out a posted 
answer is incorrect in some way, I will update that post to include a 
correction; in these cases, they will be tagged accordingly. Posts may 
come in a disordered way; use the tag features of the 
blog to impose some order.

Corrections, comments and other ways of solving a problem, are specially
welcome. Feel free to contact me personally here.

##teh statement##

Copyright (c) 2011 Roberto Ferrer

All postings and material on this blog are provided "AS IS" with no 
warranties, and confer no rights. All entries in this blog are my 
opinion and don't necessarily reflect the opinion of my employer.

All problem statements are from Paul Zeitz's The art and Craft of 
Problem Solving, Second Edition (c) John Wiley & Sons, Inc., 2007.

The rest of the content, unless otherwise noticed, is licensed under
a Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported 
License.

<h2 id="Posts-ref-zeitzps"> Posts </h2>

<ul class="posts">
  {% for post in site.categories.zeitzps %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

