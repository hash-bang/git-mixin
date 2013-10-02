Git-Mixin
=========
A handy script which manages (MixIn)[https://en.wikipedia.org/wiki/Mixin] type projects made from multiple Git repositories.

This script was originally created when I needed a way to push/pull lots of different Git repositories into the same tree.


Why was this project created
============================
As an IT company we end up writing and reusing common components all the time. Unfortunately there is no real way to bring all of these together into a project without abandoning the original repository information.

Git-Mixin is designed to track and retain what files belong to what projects and provide an easy method to pull in code from other projects but still be able to update those projects upstream if alterations/upgrades are made to the code.


Examples
========

Setup a regular project
-----------------------
Here we are setting up a standard Git controlled project using three mixins 'Alpha', 'Beta', and 'Gamma':

	# Intialize everything if we havn't already
	git init

	# Install all the mixins
	git mixin install http://path/to/alpha
	git mixin install http://path/to/beta
	git mixin install http://path/to/gamma

	# Merge the mixins into the main tree
	git mixins merge


Merge local changes back into the mixin trees
---------------------------------------------
Sometimes a change is made to a file which should be pushed upstream into the repo managing that branch.

Assuming that file-from-alpha.txt is part of the 'Alpha' project in the example above we can do:

	# This merges all mixins upstream (i.e. copies all altered files into the .git/mixins/$name directories)
	git mixins upstream

	# OR alternatively be more specific:
	git mixins upstream alpha

You can now change into the `.git/mixins/alpha` directory and push to its upstream repo as needed.


Git Config
==========
* `mixin.defaultCommand` - (default: 'owner') the command to run if just `git mixin` is run without any implied command
* `mixin.path` - (default: '.git/mixins') where the mixins are located


TODO
====
* `git mixin <install> -m` switch to perform `git mixin merge` automatically after finishing
* Ability to sub-divide a repo (have one 'super' repo which contains others as sub-directories) - Useful since GitHub limits private repos
