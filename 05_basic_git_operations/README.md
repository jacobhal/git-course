# Basic Git Operations

## What is a commit?
A commit has the same structure as a blob (object type, object length, and contents of the object).  
However, the content differs. Commits allow us to store different states of our projects. Commits are simply "wrappers" around tree objects and contains a pointer to a specific tree.  

A commit always contains
* A SHA1 hash (because it is a git object)
* Author name and email
* Commit description
* Parent

## Using the git config command to set your local git config
`git config --global user.name <Name>` - Update name for git globally  
`git config --global user.email <Email>` - Update email for git globally  
`git config --list` - View the current config

> The config information for name and email will be attatched to your commits  

## Creating a commit
1. First check your directory status using `git status`.  
2. Add the files you want to commit by moving them from your working directory to the staging area by using `git add .`. The "." adds all files to the staging area.  
3. Create a commit by using `git commit -m` and provide a commit message. Use a second "-m" to add a description as well, e.g. `git commit -m "Commit message" - "Commit description"`.  

> After the commit is created we get some information about it: which branch it was made to and the hash of the recently made commit.

## Examine the commit using low level git commands
The hash of the commit from the previous section that I made was: 5fa53d7.  
If we use `git cat-file -t 5fa53d7` we can verify that it is of type commit.  
`git cat-file -p 5fa53d7` gives us the contents of the commit, such as which tree it points to and our local git config variables for email & name.

## Various commands
`git status` - See the status of files in working directory and staging area.
`git add` - Add files to the staging area
`git commit` - Write changes to the git repository
`git log` - History of commits
`git checkout` - Checkout a specific branch or a commit

**Important command that can help trace a weird state**
`history | fgrep git` - Check the command history for all git commands

## File statuses
A git file in Git may have one of four statuses:  
* Untracked - Any new files in the working directory will be untracked (have to be staged with `git add`)
* Modified - Tracked files that are modified (have to be staged with `git add`)
* Staged - Files that are in the staging area (have to be commited with `git commit`)
* Unmodified - Files that are in the same state in the working directory as in the git repository (sync the working directory/git repository by using `git push`/`git pull`)

## Unstage files
`git rm --cached <FileName>` - Remove file from the staging area
`git reset HEAD^` or `git reset --hard` - Remove commits made but keep local changes

