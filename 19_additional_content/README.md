# Additional Content

Table of Contents
=================

   * [Additional Content](#additional-content)
      * [Git Flow](#git-flow)
      * [Cherry-picking](#cherry-picking)
         * [When to use git cherry pick](#when-to-use-git-cherry-pick)
         * [Team collaboration](#team-collaboration)
         * [Bug hotfixes](#bug-hotfixes)
         * [Undoing changes and restoring lost commits](#undoing-changes-and-restoring-lost-commits)
         * [How to use git cherry pick](#how-to-use-git-cherry-pick)
         * [Examples of git cherry pick](#examples-of-git-cherry-pick)
      * [Git bisect](#git-bisect)
         * [Git bisect in terminal](#git-bisect-in-terminal)
      * [Resetting, Checking Out &amp; Reverting (Atlassian)](#resetting-checking-out--reverting-atlassian)
         * [Git Reset vs Revert vs Checkout reference](#git-reset-vs-revert-vs-checkout-reference)
         * [Commit Level Operations](#commit-level-operations)
            * [Reset A Specific Commit](#reset-a-specific-commit)
            * [Checkout old commits](#checkout-old-commits)
            * [Undo Public Commits with Revert](#undo-public-commits-with-revert)
         * [File-level Operations](#file-level-operations)
            * [Git Reset A Specific File](#git-reset-a-specific-file)
            * [Git Checkout File](#git-checkout-file)

Created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc)

## Git Flow
Gitflow utilizes the core feature of Git, which is the power of branches. In this model, a repository has two main branches:

**Master**  
This is a highly stable branch that is always production-ready and contains the last release version of source code in production.

**Develop**  
Derived from the master branch, the development branch serves as a branch for integrating different features planned for an upcoming release. This branch may or may not be as stable as the master branch. It is where developers collaborate and merge feature branches.

> Note: The previous two branches are the starting points for any project. They are very important and should be protected against accidental deletion until the project is better defined. Only authorized leads or project owners should be given the responsibility to merge changes from other branches—such as the feature branch, which we’ll discuss later—to the develop or master branches.

Apart from those two primary branches, there are other branches in the workflow:

**Feature**  
This derives from the develop branch and is used to develop features.

**Release**  
This also derives from develop branch but is used during releases.

**Hotfix**  
This derives from the master branch and is used to fix a bug in the production branch that was identified after a release.

**Gitflow diagram**  
![Image not found](https://github.com/jacobhal/git-course/blob/master/19_additional_content/gitflow.png "Git flow diagram")

## Cherry-picking
git cherry-pick is a powerful command that enables arbitrary Git commits to be picked by reference and appended to the current working HEAD. Cherry picking is the act of picking a commit from a branch and applying it to another. git cherry-pick can be useful for undoing changes. For example, say a commit is accidently made to the wrong branch. You can switch to the correct branch and cherry-pick the commit to where it should belong.

### When to use git cherry pick
git cherry-pick is a useful tool but not always a best practice. Cherry picking can cause duplicate commits and many scenarios where cherry picking would work, traditional merges are preferred instead. With that said git cherry-pick is a handy tool for a few scenarios...

### Team collaboration
Often times a team will find individual members working in or around the same code. Maybe a new product feature has a backend and frontend component. There may be some shared code between to two product sectors. Maybe the backend developer creates a data structure that the frontend will also need to utilize. The frontend developer could use git cherry-pick to pick the commit in which this hypothetical data structure was created. This pick would enable the frontend developer to continue progress on their side of the project.

### Bug hotfixes
When a bug is discovered it is important to deliver a fix to end users as quickly as possible. For an example scenario,say a developer has started work on a new feature. During that new feature development they identify a pre-existing bug. The developer creates an explicit commit patching this bug. This new patch commit can be cherry-picked directly to the master branch to fix the bug before it effects more users.

### Undoing changes and restoring lost commits
Sometimes a feature branch may go stale and not get merged into master. Sometimes a pull request might get closed without merging. Git never loses those commits and through commands like git log and git reflog they can be found and cherry picked back to life.

### How to use git cherry pick
To demonstrate how to use git cherry-pick let us assume we have a repository with the following branch state:

```
a - b - c - d   Master
         \
           e - f - g Feature
```  

git cherry-pick usage is straight forward and can be executed like:
```
git cherry-pick commitSha
```
In this example commitSha is a commit reference. You can find a commit reference by using git log. In this example we have constructed lets say we wanted to use commit `f` in master. First we ensure that we are working on the master branch.

```
git checkout master
```

Then we execute the cherry-pick with the following command:

```
git cherry-pick f
```

Once executed our Git history will look like:

```
a - b - c - d - f   Master
         \
           e - f - g Feature
```

The f commit has been successfully picked into the feature branch.

### Examples of git cherry pick
git cherry pick can also be passed some execution options.

```
-edit
```

Passing the -edit option will cause git to prompt for a commit message before applying the cherry-pick operation

```
--no-commit
```

The --no-commit option will execute the cherry pick but instead of making a new commit it will move the contents of the target commit into the working directory of the current branch.

```
--signoff
```

The --signoff option will add a 'signoff' signature line to the end of the cherry-pick commit message

In addition to these helpful options git cherry-pick also accepts a variety of merge strategy options. Learn more about these options at the git merge strategies documentation.

Additionally, git cherry-pick also accepts option input for merge conflict resolution, this includes options: --abort --continue and --quit this options are covered more in depth with regards to git merge and git rebase.

## Git bisect
There are times when debugging just won’t cut it – you have to know when and how the bug emerged. One of the ways to do this is binary search through the commit history with git bisect, which is now available in Fork. In the menubar, choose Repository → Bisect to enter bisect mode. Checkout any commit and mark it as good or bad – Fork will remember your choice and visualize your progress in the timeline.

![Image not found](https://github.com/jacobhal/git-course/blob/master/19_additional_content/bisect.gif "Git bisect")

### Git bisect in terminal
The git bisect command works like this: 
This command uses a binary search algorithm to find which commit in your project’s history introduced a bug. You use it by first telling it a "bad" commit that is known to contain the bug, and a "good" commit that is known to be before the bug was introduced. Then git bisect picks a commit between those two endpoints and asks you whether the selected commit is "good" or "bad". It continues narrowing down the range until it finds the exact commit that introduced the change.

1. Find a good commit and type
```
git bisect start
git bisect good
```

2. Figure out where the bad commit occurred and use
```
git bisect bad
```

3. Once you have specified at least one bad and one good commit, git bisect selects a commit in the middle of that range of history, checks it out, and outputs something similar to the following:

```
Bisecting: 675 revisions left to test after this (roughly 10 steps)
```

4. You should now compile the checked-out version and test it. If that version works correctly, type

```
git bisect good
```

otherwise, type

```
git bisect good
```

5. Keep repeating the process: compile the tree, test it, and depending on whether it is good or bad run git bisect good or git bisect bad to ask for the next commit that needs testing.

## Resetting, Checking Out & Reverting (Atlassian)
The git reset, git checkout, and git revert commands are some of the most useful tools in your Git toolbox. They all let you undo some kind of change in your repository, and the first two commands can be used to manipulate either commits or individual files.

Because they’re so similar, it’s very easy to mix up which command should be used in any given development scenario. In this article, we’ll compare the most common configurations of git reset, git checkout, and git revert. Hopefully, you’ll walk away with the confidence to navigate your repository using any of these commands.

![Image not found](https://github.com/jacobhal/git-course/blob/master/19_additional_content/atlassian-images/image1.svg "Image 1")

It helps to think about each command in terms of their effect on the three state management mechanisms of a Git repository: the working directory, the staged snapshot, and the commit history. These components are sometimes known as "The three trees" of Git. We explore the three trees in depth on the git reset page. Keep these mechanisms in mind as you read through this article.

A checkout is an operation that moves the HEAD ref pointer to a specified commit. To demonstrate this consider the following example.

![Image not found](https://github.com/jacobhal/git-course/blob/master/19_additional_content/atlassian-images/image2.png "Image 2")

This example demonstrates a sequence of commits on the master branch. The HEAD ref and master branch ref currently point to commit d. Now let us execute git checkout b

![Image not found](https://github.com/jacobhal/git-course/blob/master/19_additional_content/atlassian-images/image3.png "Image 3")

This is an update to the "Commit History" tree. The git checkout command can be used in a commit, or file level scope. A file level checkout will change the file's contents to those of the specific commit.

A revert is an operation that takes a specified commit and creates a new commit which inverses the specified commit. git revert can only be run at a commit level scope and has no file level functionality.

A reset is an operation that takes a specified commit and resets the "three trees" to match the state of the repository at that specified commit. A reset can be invoked in three different modes which correspond to the three trees.

Checkout and reset are generally used for making local or private 'undos'. They modify the history of a repository that can cause conflicts when pushing to remote shared repositories. Revert is considered a safe operation for 'public undos' as it creates new history which can be shared remotely and doesn't overwrite history remote team members may be dependent on.

### Git Reset vs Revert vs Checkout reference
The table below sums up the most common use cases for all of these commands. Be sure to keep this reference handy, as you’ll undoubtedly need to use at least some of them during your Git career.

| Command	    | Scope             | Common use cases                                                      |
| -------------	| ----------------- | --------------------------------------------------------------------- |
| git reset	    | Commit-level	    | Discard commits in a private branch or throw away uncommited changes  |
| git reset	    | File-level	    | Unstage a file                                                        |
| git checkout  | Commit-level      | Switch between branches or inspect old snapshots                      |
| git checkout  | File-level	    | Discard changes in the working directory                              |
| git revert	| Commit-level	    | Undo commits in a public branch                                       |
| git revert	| File-level        | (N/A)                                                                 |

### Commit Level Operations
The parameters that you pass to git reset and git checkout determine their scope. When you don’t include a file path as a parameter, they operate on whole commits. That’s what we’ll be exploring in this section. Note that git revert has no file-level counterpart.

#### Reset A Specific Commit
On the commit-level, resetting is a way to move the tip of a branch to a different commit. This can be used to remove commits from the current branch. For example, the following command moves the hotfix branch backwards by two commits.

```
git checkout hotfix
git reset HEAD~2
```

The two commits that were on the end of hotfix are now dangling, or orphaned commits. This means they will be deleted the next time Git performs a garbage collection. In other words, you’re saying that you want to throw away these commits. This can be visualized as the following:

![Image not found](https://github.com/jacobhal/git-course/blob/master/19_additional_content/atlassian-images/image4.png "Image 4")

This usage of git reset is a simple way to undo changes that haven’t been shared with anyone else. It’s your go-to command when you’ve started working on a feature and find yourself thinking, “Oh crap, what am I doing? I should just start over.”

In addition to moving the current branch, you can also get git reset to alter the staged snapshot and/or the working directory by passing it one of the following flags:

* --soft – The staged snapshot and working directory are not altered in any way.
* --mixed – The staged snapshot is updated to match the specified commit, but the working directory is not affected. This is the default option.
* --hard – The staged snapshot and the working directory are both updated to match the specified commit.

It’s easier to think of these modes as defining the scope of a git reset operation. For further detailed information visit the git reset page.

#### Checkout old commits
The git checkout command is used to update the state of the repository to a specific point in the projects history. When passed with a branch name, it lets you switch between branches.
```
git checkout hotfix
```

Internally, all the above command does is move HEAD to a different branch and update the working directory to match. Since this has the potential to overwrite local changes, Git forces you to commit or stash any changes in the working directory that will be lost during the checkout operation. Unlike git reset, git checkout doesn’t move any branches around.


![Image not found](https://github.com/jacobhal/git-course/blob/master/19_additional_content/atlassian-images/image5.png "Image 5")

You can also check out arbitrary commits by passing the commit reference instead of a branch. This does the exact same thing as checking out a branch: it moves the HEAD reference to the specified commit. For example, the following command will check out the grandparent of the current commit:

```
git checkout HEAD~2
```

![Image not found](https://github.com/jacobhal/git-course/blob/master/19_additional_content/atlassian-images/image6.svg "Image 6")

This is useful for quickly inspecting an old version of your project. However, since there is no branch reference to the current HEAD, this puts you in a detached HEAD state. This can be dangerous if you start adding new commits because there will be no way to get back to them after you switch to another branch. For this reason, you should always create a new branch before adding commits to a detached HEAD.

#### Undo Public Commits with Revert
Reverting undoes a commit by creating a new commit. This is a safe way to undo changes, as it has no chance of re-writing the commit history. For example, the following command will figure out the changes contained in the 2nd to last commit, create a new commit undoing those changes, and tack the new commit onto the existing project.

```
git checkout hotfix
git revert HEAD~2
```

This can be visualized as the following:

![Image not found](https://github.com/jacobhal/git-course/blob/master/19_additional_content/atlassian-images/image7.svg "Image 7")

Contrast this with git reset, which *does* alter the existing commit history. For this reason, git revert should be used to undo changes on a public branch, and git reset should be reserved for undoing changes on a private branch.

You can also think of git revert as a tool for undoing committed changes, while git reset HEAD is for undoing uncommitted changes.

Like git checkout, git revert has the potential to overwrite files in the working directory, so it will ask you to commit or stash changes that would be lost during the revert operation.

### File-level Operations
The git reset and git checkout commands also accept an optional file path as a parameter. This dramatically alters their behavior. Instead of operating on entire snapshots, this forces them to limit their operations to a single file.

#### Git Reset A Specific File
When invoked with a file path, git reset updates the *staged snapshot* to match the version from the specified commit. For example, this command will fetch the version of foo.py in the 2nd-to-last commit and stage it for the next commit:

```
git reset HEAD~2 foo.py
```

As with the commit-level version of git reset, this is more commonly used with HEAD rather than an arbitrary commit. Running git reset HEAD foo.py will unstage foo.py. The changes it contains will still be present in the working directory.

![Image not found](https://github.com/jacobhal/git-course/blob/master/19_additional_content/atlassian-images/image8.svg "Image 8")

The --soft, --mixed, and --hard flags do not have any effect on the file-level version of git reset, as the staged snapshot is *always* updated, and the working directory is *never* updated.

#### Git Checkout File
Checking out a file is similar to using git reset with a file path, except it updates the *working directory* instead of the stage. Unlike the commit-level version of this command, this does not move the HEAD reference, which means that you won’t switch branches.

![Image not found](https://github.com/jacobhal/git-course/blob/master/19_additional_content/atlassian-images/image9.svg "Image 9")

For example, the following command makes foo.py in the working directory match the one from the 2nd-to-last commit:

```
git checkout HEAD~2 foo.py
```

Just like the commit-level invocation of git checkout, this can be used to inspect old versions of a project—but the scope is limited to the specified file.

If you stage and commit the checked-out file, this has the effect of “reverting” to the old version of that file. Note that this removes all of the subsequent changes to the file, whereas the git revert command undoes only the changes introduced by the specified commit.

Like git reset, this is commonly used with HEAD as the commit reference. For instance, git checkout HEAD foo.py has the effect of discarding unstaged changes to foo.py. This is similar behavior to git reset HEAD --hard, but it operates only on the specified file.
