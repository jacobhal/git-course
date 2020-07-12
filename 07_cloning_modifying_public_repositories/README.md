# Cloning, exploring and modifying public repositories

## Git clone command
`git clone <remote-repository>` - Clone a remote repository. Use either SSL or HTTPS as the remote reference.

## Large Git projects
If you clone a remote repository that is relatively large, you will notice that the .git/objects folder does not contain the folders and files that we are used to: commits, blobs and trees.  
The reason for this is that git optimizes projects and puts them into a .pack file in the pack folder. Inside the folder is also a .idx file which contains indeces for the .pack file. 

> We can unpack the pack files to see the git objects by using `cat <pack-file> | git unpack-objects`. 

## Git diff command
View changes between different versions of files by using the `git diff` command.  
You will see number of added (+)/removed (-) lines and what has changed.   
If a diff is something like `-22, 3 +22, 5`, it takes 3 lines from the old file starting from line 22 and 5 lines from the new file starting from line 22.