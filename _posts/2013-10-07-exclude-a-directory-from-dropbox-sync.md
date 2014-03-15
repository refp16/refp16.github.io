---
layout: post
title: "Exclude a directory from Dropbox sync"
description: ""
category: 
tags: []
---
{% include JB/setup %}

Dropbox does not have any explicit method for excluding a sub-directory within
the Dropbox directory, **without** deleting the local copy of that 
sub-directory.
Dropbox will allow you to exclude a sub-directory using _selective sync_ 
(from the _Preferences_ menu) but that directory will be deleted from the
local directory.

Suppose you have a place where you manage a particular project that is being
synced by Dropbox: `~/Dropbox/MyProject`. Within `../MyProject` you have 
some directory where you develop source code. Summarizing,
you have something like this:

<pre>
Dropbox
|
|--MyProject
|	|
|	|-- source
|	|    |-- classes
|	|    |-- scripts
|	|    |-- css
|	|    +--.git
|	|
|	+-- documents
|	        |-- doc1
|		|-- doc2
|		+-- doc3
|
+--OtherStuff
</pre>

If for example, you are a Git user, you probably want Dropbox to ignore `.git`
(not doing so can potentially corrupt your files), but want to keep the rest
of `MyProject` synced. Like I already mentioned, _selective sync_ can exclude
`.git` but will also delete it; for sure, an undesired consequence that will
prevent you from using version control with Git.

The strategy that can be used to bypass this behavior, assuming you have
a project directory already setup, is the following:

1. Make a copy of the `.git` directory and save it somewhere else.
2. Delete the contents of the (original) `.git` (not strictly necessary).
3. Use *selective sync* to exclude the (original) `.git` directory. Dropbox
will now delete it. 
4. Bring in the copy that was made in (1). Notice that this copy will not
be synced by Dropbox. 

You can verify using the Dropbox web account that the empty `.git` directory 
from (2) is synced but that the backup copy from (4) is not.

If you are starting a project directory from scratch, i.e. there is still no
Git repository created, manually create a .git directory (do not run 
`$ git init`) and let that be your step (2). Then proceed with other steps.

Alternatively, you could exclude the whole `source` directory if you push/pull
the project to/from a remote host like GitHub or Bitbucket. Some source files
are very small which seems to be a problem at times for Dropbox. Using a
remote host is a good idea in this case.

Keep in mind however, that if you reverse *selective sync* to include
the previously excluded directory and have a non-syncing directory with
the same name in use, then you will end up with conflicting directories 
because
Dropbox inserts a copy of the directory with exactly the same contents it had
at the moment of exclusion. 
Testing, 
I see that no files are lost. The local un-synced directory was renamed to
`whatever (Selective Sync Conflict)` and the previously excluded directory
kept the original name `whatever`. 

Another issue arises when trying
to rename a parent directory of that which is being excluded. As alredy mentioned, *Selective sync*
deletes the local version of the excluded directory but keeps a copy of it on 
its server
in some _invisible_ form. Once a rename is done, then the whole renamed
sub-tree is automatically synced because it is not recognized as an excluded
address. Additionally, a new directory is created which corresponds to an exact
copy of the sub-tree that was exluded initially. The final result is a renamed
sub-tree that is completely synced and a copy of the excluded sub-tree as it
was at the time of its exclusion. 

The previos behavior is therefore an incentive to choose a good name for
your project. One that you wouldn't want to change later on. The problems are 
not critical and the risk of data loss/corruption seems to be on the low side
but **it is** annoying.

All this works for analogous setups, not necessarily involving Git.

