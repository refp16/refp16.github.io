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
	bysort firm (year): gen diff = cond(_n == 1, 1, year - year[_n-1])
	list, sepby(firm)

Notice the `firm (year)` in the first line. This is asking Stata to sort
the data by _firm_ and _year_, but to only use _firm_ when executing the
`by`. The variable _year_ must be sorted along with  _firm_. If not, 
the subtraction on the RHS which involves _year_ and subscripting with the
_\_n_ and _\_N_ variables would make no sense. In particular, we want to 
compute the difference between **consecutive** or neighbouring years within
firms, and sorting by _firm_ _year_ guarantees just that. 

So an immediate thing to think about when `(varlist)` appears on the
LHS, is that _varlist_ must be critical for the computation being done 
in the RHS. The `generate` command, however, we want to execute for each _firm_.
The previous code produces:

	     +----------------------------+
	     | year   firm   sales   diff |
	     |----------------------------|
	  1. | 2000      1      36      1 |
	  2. | 2001      1      45      1 |
	  3. | 2002      1      39      1 |
	     |----------------------------|
	  4. | 2000      2      42      1 |
	  5. | 2001      2      42      1 |
	  6. | 2002      2      36      1 |
	     |----------------------------|
	  7. | 2000      3      14      1 |
	  8. | 2002      3      11      2 |
	     |----------------------------|
	  9. | 2000      4      12      1 |
	 10. | 2001      4      12      1 |
	 11. | 2002      4       9      1 |
	     |----------------------------|
	 12. | 2001      5      10      1 |
	 13. | 2002      5       7      1 |
	     +----------------------------+

