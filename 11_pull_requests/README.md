# Pull requests
Pull requests are a proposal of the potential changes.  

The main idea behind naming it "pull" request is that another person should pull the potential changes and see if it looks good and works. If it does, that person can approve the pull request.
However, the more common way is to just simply make a code review on Github/Azure DevOps/Bitbucket etc. and then approve the changes and assume that the tests will fail if it does not work.

## Merge request vs pull request
If you simply want to merge one of your feature branches into another branch the name merge request would be more appropriate but it is still called a pull request in most cases.  
If you want to contribute to an open source repository the name pull request is more appropriate since you have to create a copy of the codebase, create a feature branch and then ask an author of the original repository to pull in your changes.

**Contributing to an open source repository**
![Image not found](https://github.com/jacobhal/git-course/blob/master/11_pull_requests/fork-contribution.png "Fork contribution")

## Pull request process
**Step 1**
![Image not found](https://github.com/jacobhal/git-course/blob/master/11_pull_requests/step-1.png "Step 1")

**Step 2**
![Image not found](https://github.com/jacobhal/git-course/blob/master/11_pull_requests/step-2.png "Step 2")

**Step 3**
![Image not found](https://github.com/jacobhal/git-course/blob/master/11_pull_requests/step-3.png "Step 3")

> Note that an existing pull requests is automatically updated when new commits are pushed to remote

**Step 4**
![Image not found](https://github.com/jacobhal/git-course/blob/master/11_pull_requests/step-4.png "Step 4")

> Note that you can set number of people that have to approve the pull request (and other rules if you want to).

**Step 5**
![Image not found](https://github.com/jacobhal/git-course/blob/master/11_pull_requests/step-5.png "Step 5")

> Note that not every person might have permission to perform the merge. In large teams only a few selected people might have that authority.

## Overwrite the last commit made
`git commit --amend` - Overwrite the previous commit with this one  
`git commit --amend --author="Jacob Hallman <test@gmail.com>` - Overwrite previous commit and change the author of it

## List config variables
`git config --list`

## Add comments and approve pull request
On Github or any other Git repository tool you can comment on pull requests and make sure that some have to be resolved before it is approved.

*Add single comment* - Add a single comment and the author will get notified about it immediately.
*Start a review* - Add multiple comments and the author will get one notification for all commets.

> Note that you can also go to the "File changes" tab and either *Comment, Approve or Request changes*.

## Merging pull requests
There are different ways to merge pull requests.  

**Create a merge commit**
All the commits from the feature branch will be added to the base branch with a merge commit. All history will be preserved and the merge commit will have 2 parents: the last commit on the base branch and the last commit on the feature branch.

**Squash and merge**
The commits from the feature branch will be combined into one commit in the base branch.

**Rebase and merge**
The commits from the feature branch will be rebased and added in the base branch.

> See more about squash and rebase in later more advanced sections.

## Adding new collaborator to Github repository
Settings --> Collaborators

## Configuring branch rules on Github
Settings --> Branches --> Branch protection rules

> Rules such as preventing direct pushes, prevent deletion, require status checks before merging can be added here

## Working with issues on Github
