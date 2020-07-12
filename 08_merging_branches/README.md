# Merging branches
When you want to incorporate changes made in one branch into another, we use merging.  
There are two ways of merging: fast-forward merge and 3-way merge.

## Git merge command
`git merge <feature-branch>` - Merge feature-branch into the branch that is currently checked out

## Fast-forward merge
Fast-forward merge is possible when there are no further commits in the receiving branch after the commit where the feature branch was created.  

To merge the feature branch into master in the example below, follow these steps:  
1. Checkout master branch so that HEAD is pointing to master.
2. Select which branch you want to merge into master (git will check if there are any more commits on the master branch since the feature branch was created).
3. Fast-forward merge is performed by moving (or fast-forwarding) the master branch pointer to the latest commit on the feature branch.

**Before merge**
![Image not found](https://github.com/jacobhal/git-course/blob/master/08_merging_branches/fast-forward-before.png "Fast-forward before merge example")

**After merge**
![Image not found](https://github.com/jacobhal/git-course/blob/master/08_merging_branches/fast-forward-after.png "Fast-forward after merge example")

## 3-way merge
3-way merge is necessary if there are further commits in the receiving branch after the commit where the feature branch was created. If we fast-forward we would lose the information of all the new commits on the receiving branch.

To merge the feature branch into master in the example below, follow these steps:  
1. Checkout master branch so that HEAD is pointing to master.
2. Select which branch you want to merge into master (git will check if there are any more commits on the master branch since the feature branch was created).
3. 3-way merge is performed by taking the *Ancestor* commit (the latest common commit between the two branches) and the latest commit on each branch and creates a new *Merge commit*. Notice that the new merge commit has two parents, the latest commit on either branch used in the merge process. The feature branch can then be safely removed because the merge commit has the latest commit on the feature branch as a parent.

> If you are using a mergetool such as KDiff3, the Ancestor is called *Base* or *A*, the receiving branch *Local* or *B* and the branch being merged *Remote* or *C*.

**Before merge**
![Image not found](https://github.com/jacobhal/git-course/blob/master/08_merging_branches/3-way-merge-before.png "3-way before merge example")

**After merge**
![Image not found](https://github.com/jacobhal/git-course/blob/master/08_merging_branches/3-way-merge-after.png "3-way after merge example")



## Sourcetree/Fork
Sourcetree and Fork are two similar visual Git tools that are popular.

## Merge conflicts
Merge conflicts happen when the same files are edited in both of the branches that we are trying to merge.

**Merge conflict example**
![Image not found](https://github.com/jacobhal/git-course/blob/master/08_merging_branches/merge-conflicts.png "Merge conflict example")

`git ls-files -s` - List files in the staging area. The files with conflicts will have 3 copies with numbers 1, 2 and 3.

> 1 = Base, 2 = Local, 3 = Remote

> During the merging process, git creates another HEAD file called MERGE_HEAD. This is a reference to the last commit of the feature branch that we are merging.

**git log after merge conflict**
![Image not found](https://github.com/jacobhal/git-course/blob/master/08_merging_branches/merge-conflicts-git-log.png "Merge conflict example")

