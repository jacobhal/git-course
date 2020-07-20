# Github Pages
You are able to create static websites hosted on Github with Github Pages (kind of like Heroku).  
Your website will be a subdomain to github.io or you could connect your custom domain to your Github page.

## Create a simple website using Github Pages
1. Create a new public repository on Github with the following naming convention: <username>.github.io
2. Create a simple index.html and see your website at url <username>.github.io

## Enable Github Pages for an existing repository
Settings --> Github Pages section --> source --> master branch

> See the link to the website by scrolling down to Github Pages section again and copy the hosted website link.

## Automating the React build step for React applications
There are several options to automate this process. For my own website I use the git-ftp package in order to automatically push changes from master.

> By using Github Pages you can use the NPM package gh-pages and set predeploy/deploy steps as package.json scripts.

## Configuring a custom domain for Github Pages

