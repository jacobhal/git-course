# Git branches and HEAD

## What are branches?
* Branches are just text references to a specific commit.  
* Pointers for all branches are located in **.git/refs/heads**.  
* The branch pointer moves automatically after every new commit.  

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

See the image below

![Image not found](https://github.com/jacobhal/git-course/blob/master/06_git_branches_and_head/Branches.png "branches example")