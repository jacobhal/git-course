# Detached HEAD
You move into detached HEAD state when you checkout a specific commit instead of a branch.  
In such a state you can make experimental commits that will be garbage collected once you checkout a specific branch.

## Retaining changes made in detached HEAD state
`git checkout -b <branch-name>` - Retain experimental commits in a new branch