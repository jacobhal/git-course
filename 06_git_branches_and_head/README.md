# Git branches and HEAD

## What are branches?
* Branches are just text references to a specific commit.  
* Pointers for all branches are located in **.git/refs/heads**.  
* The branch pointer moves automatically after every new commit.  

`git branch` - List all local branches  
`git branch -r` - List all remote branches  
`git branch -a` - List both local and remote branches  
`git branch -vv` - List all branches and corresponding remote branches.  
`git branch <name>` - Create a new branch  
`git branch -d <name>` - Delete a branch (it has to be merged, if you want to force delete it use `-D` instead)  
`git branch -m <old-branch> <new-branch>` - Rename a branch  
`git checkout <branch>` - Switch to an existing branch  
`git checkout -b <branch>` - Create a new branch and switch to it  
`git checkout -b <new-branch> <existing-branch>` - Create a new branch and switch to it BUT base it on an existing branch other than the current  

## What is HEAD?
HEAD is a reference to the currently checked-out branch or commit. We can only have one HEAD.  
* Head is only locally significant
* The HEAD pointer is stored in **.git/HEAD**
* The default pointer is ref: refs/heads/master
* Change the HEAD reference to a specific branch with `git checkout <branch>`
* Change the HEAD reference to a specific commit with `git checkout <SHA1>`

> Type in `cat refs/heads/master` to see the hash of the commit that master is pointing to

### Detached HEAD
If HEAD points directly to a commit instead of the current branch, it will be *detached*.

## VIM Editor
The default VIM editor can be confusing. If you type in `git commit` and omit the -m message, you will be directed to your default git editor to type in a message + optional description. If that is VIM, type your commit message and then type `:wq` to save and exit.

## Git branches management
We need branches to work on different features while keeping the master (or development etc. if using Git Flow) branch clean.

Branch management example with two feature branches: BR-102 and exp

![Image not found](https://github.com/jacobhal/git-course/blob/master/06_git_branches_and_head/branches.png "branches example")

## Reusing blobs
Git resuses blobs if they have the same content. file4.txt in this folder is the same as file1.txt in folder 04_git_under_the_hood so we can use the same hash that was created before. The new tree in BR-1 contains a pointer to an existing blob for file4.txt.