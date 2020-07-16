# Git tags
Git tags are static text pointers to specific commits unlike branches that are dynamic pointers.  
You can create tags anywhere and whenever you want.  

Tags are mostly used to handle release versions for your project.  
For instance, when any of the major feature branches are merged into master, a new release tag may be added.

## Garbage collector
Commits made in detatched HEAD state will be removed by the garbage collector if you checkout any other branch.

## Staging vs Production

### Continuous Integration (CI) and Continuous Development (CD)
Software development in the real world is often done using the CI/CD principle, which means that development follows a continuous delivery pipeline.

There are typically two environments that development occurs in: Staging and Production.  
In Git, you can easily separate those two by using two different branches.  

> Usually a branch called "release" is used for staging and "master" is used for production.

**A comparison of the staging environment and production environment**
![Image not found](https://github.com/jacobhal/git-course/blob/master/13_git_tags/staging-vs-production.png "Staging vs production")

## Semantic versioning
Semantic versioning is important when developing ANY KIND of software. It is extremely common, and you should know about it as a software developer.  

A version in semantic versioning can look like this: v5.1.3  
5 = Major version  
1 = Minor version  
3 = Patch version

**Major version**   
Major versions include implementing new features that makes the next version of the software incompatible with previous versions and include major changes.  

A new major version "resets" minor and patch versions: 5.1.3 --> 6.0.0  

**Minor version**  
Minor versions are any small features that adds some additional functionality to the software but does not break any previous versions. So any software that relies on your software does not break on a new minor version.  

A new minor version "resets" the patch version: 5.1.3 --> 5.2.0

**Patch version**  
Patch versions are usually small bug fixes or feature adjustments. 

A new patch version looks like this: 5.1.3 --> 5.1.4


Link for semantic versioning: https://semver.org  

### Prerelease version
If you are developing any new feature and you have a staging environment where you test new features, you can use prerelease versions like these: 5.2.4-alpha, 5.2.4-beta or 5.2.4-1.3

> A release version without prerelease numbers is greater than a release version with prerelease numbers: 5.2.4 > 5.2.4-1.3

## Lightweight vs annotated tags
`git tag` - List all tags
`git show <tag-name>` - Show the specific tag (information about the commit it is tied to)

**Lightweight**  
* `git tag v1.0.0` - Create a lightweight tag
* Is stored in .git/refs/tags

**Annotated**  
* `git tag -a v1.0.0 -m "New tag"` - Create an annotated tag
* Is stored in .git/refs/tags
* Is also stored in .git/objects
* Stores tag message
* Stores tag author and date

`git tag -v <tag-name>` - Shows the hash of the commit object the tag points to  
`cat .git/refs/tags<tag-name>` - Shows the hash of the tag itself  
`git cat-file -t <tag-hash>` - Outputs type tag  
`git cat-file -p <tag-hash>` - Outputs the content of the tag  

> Tags are not pushed to the remote repository by default.

## Pushing tags to remote
`git push --tags` - Push ONLY tags to remote repository

## Create releases on Github
Releases --> Draft a new release

