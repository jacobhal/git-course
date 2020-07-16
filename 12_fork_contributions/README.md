# Forks and contributions to a public repository
A fork is a copy of another repository. By creating a copy we can create any remote branches we want and then make pull requests to the original repository.

## Creating a fork
1. Go to Github.
2. Go to the repository you want to fork and press "Fork". This will create a copy of the repository in your own repositories.
3. You can then clone the forked repository like you would any other.

> Type `git remote -v` to see that the forked repository is linked to your own repositories and not the original.

## Sync a forked repository with parent repository
`git remote` tells us that the only remote server configured for our forked repository is origin but we want to include the parent repository here as well.  
What we want to do is to add another remote server called upstream for our parent repository so that we can pull directly from upstream.  
We want it to look like the diagram below.

**Upstream example diagram**

![Image not found](https://github.com/jacobhal/git-course/blob/master/12_fork_contributions/upstream-example.png "Setup upstream example")

## Adding upstream to parent repository
You can add an upstream to the parent repository using the command below:    
`git remote add upstream <clone-url-of-parent-repository>`

> Type `git remote` in order to see both origin and upstream.

## Synchronize changes from upstream
1. `git pull upstream master` - Pull changes from upstream  
2. `git push` - Push to origin in order to sync changes (no need to specify origin if it is a tracking branch)

## Create a pull request from the forked repository
1. Click either "Compare & pull request" or go to branches and create it from there.
2. "compare across forks" will alternate between making pull requests in your forked repository and the parent repository.
3. Choose the remote base repository and branch that you want to make a pull request against.
4. Choose if you want maintainers of the base repository to be able to make code changes in your pull request by checking/unchecking "Allow edits from maintainers".

