# Git push, fetch and pull

## Commands overview
`git fetch`, `git push` and `git pull` are necessary in order to communicate with a remote repository.  
See the diagram below to see where they fit.

**Commands overview**
![Image not found](https://github.com/jacobhal/git-course/blob/master/10_git_push_fetch_pull/commands-overview.png "Commands overview")

You should only push to remote repository when changes have been tested locally.

## What is origin?
How is a remote repository connected to your local repository? By default, when you clone a remote repository git automatically creates a binding between the local repository and remote repository.

The default name of the remote repository is **origin**.

You can link multiple remote repositories to a local repository. If you do for instance `git pull`, you automatically pull from the origin.

### Examine list of remote repositories locally
`git remote` - List all remote repositories
`git remote -v` - List all remote repositories connected to your local repository for fetch and push operations.

## List remote and local branches
Git does not automatically create local branches for your remote branches, only the default one.
`git branch -r` - List all remote branches
`git branch -a` - List both local and remote branches

You will see something like `remotes/origin/HEAD -> origin/master`.  
First we have a prefix "remotes" which indicates that it is a remote branch.  
Second we have "origin", which is the remote git server/repository.  
Third comes name of the branch but first comes the HEAD and what branch it points to.

## Tracking branch
Tracking branch is your local branch that is connected to a specific remote branch. When you clone a repository, git automatically creates the first tracking branch, master. master is connected to the remote master branch.  

In the diagram below, the tracking branches are master, release and BR-2.

![Image not found](https://github.com/jacobhal/git-course/blob/master/10_git_push_fetch_pull/tracking-branches.png "Tracking branch example")

`git branch -vv` - List all branches and corresponding remote branches.
`git checkout <remote-branch-name>` - Checkout on a remote branch automatically creates a local tracking branch.

## git remote show origin
`git remote show origin` - Show information about the remote origin git server.

## Pruning branches
If a remote branch is removed, the tracking branch reference becomes stale since it no longer has a reference to a remote branch. If you push changes from your locally untracked branch, it will create another remote branch and become tracked.

`git remote prune origin` - Prune the origin to remove the remote branch reference (the local branch will still be available even if the reference to the remote is gone).

## Fetch, pull and push
`git fetch` - Fetch changes from the remote server but do not merge them
`git pull` - Fetch changes from remote branch and merge them into current branch
`git push` - Push local changes to remote server

**Git pull step-by-step**
1. Checkout local branch and make sure that it is a tracking branch and has a corresponding remote branch. Use `git branch -vv` to check that this is the case.
2. Enter `git pull`.
3. Git will fetch all changes from the remote repository - `git fetch` is executed in the background.
4. After fetching, Git updates the FETCH_HEAD file that contains SHA1 hashes of last commits in the remote repository for all tracking branches.
5. Git merges remote branch into current branch with `git merge FETCH_HEAD`.

## FETCH_HEAD


## Resolve conflicts during git pull

## Git show-ref