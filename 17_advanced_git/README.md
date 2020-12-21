# Advanced Git

## Git log
`git log --oneline` - See a collapsed view of all commits and go through commits one by one  
`git log --graph` - See a graphical view of the commit tree  
`git log --stat` - See more statistics in each commit, for example the quantity of the changes, how many files changed etc.  
`git log -p` - See the actual changes in every file (not that useful in terminal)  
`git log -4` - See the last 4 commits

### Git shortlog
`git shortlog` - See a summary of all commits in the repository, which authors have made most commits etc.  
`git shortlog -n` - Same as above but ordered by most active authors  
`git shortlog -n -s` - See the count for each author but do not view commits  


### Filter commits by author or keyword
`git log --author="<author-name>"` - Filter commits by author  
`git log --grep="<search-query"` - Find commits that contains <search-query> in commit message/description  

### Pretty formatting of git log
`git log --pretty=format: "%H"` - See SHA1 hashes only  
`git log --pretty=format: "%cn H"` - See commiter name and SHA1 hashes only  

### Filter out merge commits from git log
`git log --merges` - See only merge commits  
`git log --no-merges` - See only non-merge commits  

## Git reset
git reset is a destructive command since it alters history. Avoid using it on public branches. 
By resetting you can reset to any commit in your history. Any commits after the commit you reset to will be kept in working directory by default.

`git reset <SHA1-hash>` - Allows you to discard commits that you have made and get back to a previous state of the repository  
`git reset --mixed <SHA1-hash>` - Discard commit/commits. Discard changes in staging area (index). Keep changes in working directory (this is the default option).  
`git reset --soft <SHA1-hash>` - Discard commit/commits. Keep changes in staging area (index). Keep changes in working directory (this is the default option).  
`git reset --hard <SHA1-hash>` - Discard commit/commits. Discard changes in staging area (index). Discard changes in working directory (this is the default option).  
`git reset --hard HEAD` - Discard all changes you have made locally and go back to the state of HEAD.  

**Important**  
`git reset --hard origin/<BranchName>` - Reset a local branch to the state of a remote branch.

## Git revert
git revert is NOT a destructive command since it does not alter history unlike git reset. Thus, it can be safely used on public branches.

`git revert <SHA1-hash>` - Allows you to discard ONE single commit by reverting all the changes made in the commit and add a brand new one to apply the changes.  
`git revert HEAD` - Discard the last commit.

## Modyfing last commit by using amend
This option is useful if you have made typos or mistakes in the very last commit. Git will create a brand new commit and the previous one will be garbage collected. Thus, --amend is a destructive operation and should only be used on private branches.

`git commit --amend` - Amend the last commit and update the commit message  

## Cherry-picking commits
Cherry-picking allows you to take any commit and insert it into the currently checked out branch as a new commit. Cherry-picking can be used if you are working on a separate feature branch and have made a separate commit for a bug fix but you are not yet finished with the feature. Then you can cherry-pick that specific commit into master/development etc. in order to only add the bug fix changes.

`git cherry-pick <SHA1-hash>` - Cherry-pick and insert commit with <SHA1-hash> into currently checked out branch  
`git cherry-pick --no-commit <SHA1-hash>` - Cherry-pick without automatically creating a new commit

## Reflog - log of all Git operations
This is a very useful command that shows operations that have been used locally. Git reflog allows you to revert back to previous states. Let's say you made a git revert to discard the 5 last commits, then you can use git reflog to get them back.

`git reflog` - See a list of operations made
`git reflog show <branch-name>` - See the reflog of a specific branch

You can use the HEAD pointers like *HEAD@{10}* from git reflog as references instead of specific commit hashes.

### Example usage
1. `git lg` - See the git commit history and choose some commit in history, copy the SHA1-hash.
2. `git reset --hard <SHA1-hash>` - Make git point to that previous commit.

To undo the above operation, type `git reflog` and then use `git reset--hard <SHA1-hash>` to the hash before the reset was made.

## Stashing
If you have local changes that are not yet committed but you want to checkout another branch and keep the changes you have made in your current branch, then you can use stashing. Stashing saves uncommitted work.

`git stash` - Stash your local changes in a git object (remove them and save them for later)  
`git stash pop` - Apply the changes from the last git object that was stashed

## Garbage collection
`git gc` - Manually perform Git garbage collection (removes old references, compresses objects to take up less space by using a .pack file etc.)


