Git-Bundle
==========
A handy script which manages (MixIn)[https://en.wikipedia.org/wiki/Mixin] type projects made from multiple Git repositories.

This script was originally created when I needed a way to push/pull lots of different Git repositories into the same tree.


Examples
========

Setup a regular project
-----------------------
Here we are setting up a standard Git controlled project using three mixins 'Alpha', 'Beta', and 'Gamma':

	# Intialize everything if we havn't already
	git init

	# Install all the bundles
	git bundle install http://path/to/alpha
	git bundle install http://path/to/beta
	git bundle install http://path/to/gamma

	# Merge the bundles into the main tree
	git bundle merge


Merge local changes back into the bundle trees
----------------------------------------------
Sometimes a change is made to a file which should be pushed upstream into the repo managing that branch.

Assuming that file-from-alpha.txt is part of the 'Alpha' project in the example above we can do:

	# This merges all bundles upstream (i.e. copies all altered files into the .git/bundle/$name directories)
	git bundle upstream

	# OR alternatively be more specific:
	git bundle upstream alpha

You can now change into the `.git/bundle/alpha` directory and push to its upstream repo as needed.


TODO
====
* `git bundle own` - Show a list of which bundles own what files, also allocate a file into a bundle (e.g. `git bundle own <bundle> <file>`)
* `git bundle <install> -m` switch to perform `git bundle merge` automatically after finishing
* Ability to sub-divide a repo (have one 'super' repo which contains others as sub-directories) - Useful since GitHub limits private repos
