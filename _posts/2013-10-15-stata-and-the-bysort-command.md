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

And again, we want to `sort` by _firm_ and _diff_, but `drop` a _firm_ group.
It may not be obvious the need to sort _diff_ in this example, 
but consider the case in which

	     |----------------------------|
	  7. | 2000      3      14      1 |
	  8. | 2002      3      11      2 |
	     |----------------------------|

was instead

	     |----------------------------|
	  7. | 2000      3      14      1 |
	  8. | 2004      3      11      4 |
	  9. | 2005      3      18      1 |
	     |----------------------------|

Note that the way in which we identify jumps for a firm is looking for
 _diff_ > 1.
To be able to reliably locate a jump, we have to sort _diff_ in ascending
order so that the high numbers end up at the end. In particular, check the last
one (_\_N_) and see if it is higher then 1. If so, there's at least one jump.
If not, then all previous numbers must equal 1 and there are no jumps. 

The result of executing Step 2 is

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
	  7. | 2000      4      12      1 |
	  8. | 2001      4      12      1 |
	  9. | 2002      4       9      1 |
	     |----------------------------|
	 10. | 2001      5      10      1 |
	 11. | 2002      5       7      1 |
	     +----------------------------+

Going back to our original example, if we were to use:

    * Step 2 (alternative 1)
    bysort firm: drop if diff[_N] > 1
    list, sepby(firm)

we would get the same correct result. But this code is not general since
it is only by chance that _diff_ is already sorted in ascending order.
If we were to apply this in a realistic setting, we would almost surely
end up with undesired consequences.

Finally, we could try

    * Step 2 (alternative 2)
    bysort firm diff: drop if diff[_N] > 1
    list, sepby(firm)

This alternative presents _diff_ **without** the parenthesis. As before, 
we are sorting _firm_ _diff_ but we are also dropping observations using
groups made by these two variables. Unlike the previous cases where the
`drop` applies to groups of _firms_, effectively ridding all observations
of a firm with jumps, here we delete only those observations of a firm that 
comply with the `if` condition individually. Potentially, we are leaving behind
observations that belong to firms with jumps.

The following result confirms this:

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
	     |----------------------------|
	  8. | 2000      4      12      1 |
	  9. | 2001      4      12      1 |
	 10. | 2002      4       9      1 |
	     |----------------------------|
	 11. | 2001      5      10      1 |
	 12. | 2002      5       7      1 |
	     +----------------------------+

Notice how one observation for firm 3 managed to survive the `drop`.
This was not intended.

All this speaks of the importance of getting the `bysort`s right. 

###Appendix###

The complete code:

	* ------------------------------ input -----------------------------------------
	clear
	input year firm sales
	2000 1 36
	2000 3 14
	2000 2 42
	2000 4 12

	2001 1 45
	2001 2 42
	2001 4 12
	2001 5 10

	2002 1 39
	2002 2 36
	2002 3 11
	2002 5 7
	2002 4 9
	end
	sort firm year
	list, sepby(firm)

	* ----------------- delete firms with jumps in time series ---------------------

	* Credit: Nick Cox

	* Step 1
	bysort firm (year) : gen diff = cond(_n == 1, 1, year - year[_n-1])
	list, sepby(firm)

	preserve

		* Step 2
		bysort firm (diff): drop if diff[_N] > 1
		list, sepby(firm)

	restore

	* ------------------------- incorrect alternatives------------------------------

	preserve

		* Step 2 (alternative 1)
		bysort firm: drop if diff[_N] > 1
		list, sepby(firm)

	restore

	preserve

		* Step 2 (alternative 2)
		bysort firm diff: drop if diff[_N] > 1
		list, sepby(firm)

	restore

	* ------------------------------------------------------------------------------

