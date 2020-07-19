# Ignoring files in Git
You can tell Git to explicitly ignore certain files or folders.  
Any changes in the files and folders are ignored as well.

Such rules are defined in a file called .gitignore which must be committed.

## Git file statuses
![Image not found](https://github.com/jacobhal/git-course/blob/master/15_gitignore/file-statuses.png "File statuses")

## Basic gitignore rules
`file.txt` - Ignore single file

`bin/` - Ignore entire folder

`*.tmp*` - Ignore all files with .tmp extension

## Committing previously ignored file
Just remove the certain rule that ignores the file from the .gitignore and Git will start to track it.

## Ignore previously committed file
Option 1:
1. Add ignore rule to .gitignore
2. Delete file in working directory
3. Commit changes
4. Re-add the previously deleted file

Option 2:
1. Add ignore rule to .gitignore
2. Delete the file from repository only but keeping it in the working directory by using `git rm --cached <file name>`

## Git ignore common practices and templates
* Build folders like /bin
* Dependency folders like /node_modules
* Compiled and log files like *.pyc, *.log
* Hidden OS files like Thumbs.db or .DS_STORE 

Create or see default .gitignore templates:
https://www.toptal.com/developers/gitignore
https://github.com/github/gitignore


