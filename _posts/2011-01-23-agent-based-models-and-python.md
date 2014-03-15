---
layout: post
title: "Agent-based models and Python"
description: ""
category: 
tags: []
---
{% include JB/setup %}

About two months ago I swore I would start doing **all** my work with just **one** high-level programming language, instead of jumping around from one specific software to another. This, I thought, is going to be rough at the initial phase (I’m no programmer) but will eventually payoff with expertise knowledge of a product that will let me create virtually anything.

After some research, Python (I thought again), is what I’m looking for. Because at the moment I was also picking up on the paradigm of agent-based modeling (ABM) I demanded myself I learn how to do this stuff using Python.

Python implementations of ABM, I must say, are not abounding in the web. However, I managed to find some resources on the subject that I’d like to share:

- [Professor Pietro Terna](http://href.li/?http://web.econ.unito.it/terna/) has an [interesting contribution](http://href.li/?http://eco83.econ.unito.it/terna/slapp/) where he uses Python code to do ABM following the [Swarm](http://href.li/?http://www.swarm.org) framework (Swarm is an Objective-C based ABM simulation environment). Because Swarm is not just about the code but  has also a general conceptual framework for ABM, it lends itself to being ported to other languages. Professor Terna calls it SLAPP (Swarm-Like Agent Based Protocol in Python).

- [Simpy](http://href.li/?http://simpy.sourceforge.net/), which is an “object-oriented, process-based discrete-event simulation language” (module) for Python is another way of doing ABM in Python. Although I found no examples of applications in the realm of social sciences, I was able to write a [short example code](https://gist.github.com/refp16/7399430) in which agents move around randomly about a grid. 

- [Professor Downey](http://www.olin.edu/faculty/faculty_profile.aspx?FacultyId=13) has written [Swampy](http://www.greenteapress.com/thinkpython/swampy/), a suite of Python programs for use with [_Think Python_](http://href.li/?http://thinkpython.com/thinkpython.html), [_Python for Software Design_](http://href.li/?http://thinkpython.com/), and [_The Little Book of Semaphores_](http://href.li/?http://greenteapress.com/semaphores). Its components are made of small, documented programs that underlie the basics of ABM. I find it specially useful if you want to include GUIs in your simulations.

- Finally, [Professor Simon Frost](http://www.vet.cam.ac.uk/directory/sdf22@cam.ac.uk) has done some work on Epidemiology using ABM and Python. He has made available his source code at [Google code](http://code.google.com/p/simonfrost/downloads/list).

As to my oath,  I’m afraid I already cracked. I still plan on learning everything I can about Python, but I decided I’d give a chance to [NetLogo](http://href.li/?http://ccl.northwestern.edu/netlogo/) for a while. If you’re on the low side of programming proficiency and want hands-on experience with the making of ABM (with quick, great results), give it a try. I’m sure it will even help with organizing your thoughts on ABM if you feel the need of using another programming language to get the job done.
