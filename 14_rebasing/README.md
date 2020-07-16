# Rebasing
Very often if you are working on a local branch you need to merge master/release branches into your local branch in order to keep it up to date with published features. In such cases you can use rebasing.

> Remember to NEVER use rebasing on public branches such as master or release because it is a potentially destructive operation that changes history.

**Advantages of rebasing**  
* History becomes linear, with merging there are commits that have multiple parents but with rebasing every commit only has 1 single parent.

**Disadvantages of rebasing**  
* Rewrites history, doesn't keep entire history of commits. Some commits are acutally lost during rebasing, you cannot travel back in time and check commits on specific branches that were rebased.

## Merging vs Rebasing

**3-way merge recap**  
![Image not found](https://github.com/jacobhal/git-course/blob/master/14_rebasing/3-way-merge.png "3-way merge")

**Rebasing history vs merging history**  
![Image not found](https://github.com/jacobhal/git-course/blob/master/14_rebasing/rebase-vs-merge.png "Rebase vs merge")

## How to perform rebasing
Rebasing is a two-step process. The first two steps in the process below would be the first step and the latter two the second.

**Rebase process**  
![Image not found](https://github.com/jacobhal/git-course/blob/master/14_rebasing/rebase-process.png "Rebase process")

**Step 1**  
Git creates "copies" of the commits from the feature branch and puts them onto master to achieve a linear history. The feature branch pointer is moved to the last of the copied commits.
![Image not found](https://github.com/jacobhal/git-course/blob/master/14_rebasing/step-1-rebase.png "Rebase step 1")

**Step 2**  
Git moves the master pointer to the same place as our feature pointer, thus we get our linear history.
![Image not found](https://github.com/jacobhal/git-course/blob/master/14_rebasing/step-2-rebase.png "Rebase step 2") 

**Rebase process in Fork**   
In order to rebase feature1 onto master:  
1. Perform rebasing by checking out feature1, then right-clicking the master branch and select "Rebase Interactively 'feature1' to Here".
1. (Alternative) In the branches outline to the left, drag feature1 onto master and select "Rebase Interactively 'feature1' on 'master'".
2. 

**Change the commit message of a commit using Rebase**  
Way 1: Right click the commit --> Interactive Rebase --> Reword Message  
Way 2: Rebase <branch-name> interactively to here --> Click 3 dots of commit --> Edit message

**Reorder commits using Rebase**  
Way 1: Right click the commit --> Interactive Rebase --> Edit --> Move commits up and down with CMD + Up/Down arrows or drag and drop  
Way 2: Rebase <branch-name> interactively to here --> Move commits up and down with CMD + Up/Down arrows or drag and drop  

**Combine multiple commits into one using Rebase**  
Right click the commit --> Interactive Rebase --> Squash into parent (groups the current commit together with the last one)

## Explore graph and commits in Fork/Sourcetree

Temporary text