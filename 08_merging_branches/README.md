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


## Sourcetree/Fork

## Merge conflicts