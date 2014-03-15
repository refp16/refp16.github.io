---
layout: post
title: "Stata and the bysort: command"
description: ""
category: 
tags: [stata]
---
{% include JB/setup %}


Until today, for some reason, I misunderstood the precise workings of the
Stata command `bysort`. As its name suggests (and as explained by 
`help bysort`), it's only the `by` with a `sort` option. That sounds pretty
easy. The syntax however,
I found confusing when it included the `(varlist)` option. Now I wonder why. 
I must have read the help file carelessly in the past.

Today I ran into [this post](http://www.stata.com/statalist/archive/2013-10/msg00498.html) 
at the Statalist Archive. After playing around with a response, I 
finally came to grips with the command.

The query was on how to eliminate _firms_ in a panel database if they presented
jumps along the _year_ variable. For example, start with a 
database that looks like this:

	     +---------------------+
	     | year   firm   sales |
	     |---------------------|
	  1. | 2000      1      36 |
	  2. | 2001      1      45 |
	  3. | 2002      1      39 |
	     |---------------------|
	  4. | 2000      2      42 |
	  5. | 2001      2      42 |
	  6. | 2002      2      36 |
	     |---------------------|
	  7. | 2000      3      14 |
	  8. | 2002      3      11 |
	     |---------------------|
	  9. | 2000      4      12 |
	 10. | 2001      4      12 |
	 11. | 2002      4       9 |
	     |---------------------|
	 12. | 2001      5      10 |
	 13. | 2002      5       7 |
	     +---------------------+

Firm 3 presents a jump because there is no year 2001. So the question is 
how do we check for these jumps and delete firms that present this feature.
Nick Cox suggests the following:

    * Step 1
	bysort firm (year): gen diff = cond(\_n == 1, 1, year - year[n-1])
	list, sepby(firm)


