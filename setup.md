---
layout: default
title: {{ site.name }}
---

# <a name="setup" class="anchor">Setup</a>
 
These instructions are intended for users of Mac OS X or other Linux/Unix systems. You will need to have commandline git and Ruby installed (which we will not cover here). Mac OS X comes with git and Ruby installed however you may need a newer version of Ruby (upgrading the system's default Ruby is not recommended). In this case, you can try using [RVM](https://rvm.io/rvm/install) or another Ruby version manager to install a different version of Ruby on your machine.

## <a name="" class="anchor">Creating New Orphan Branches</a>
In terminal, navigate to your code repository directory. In our case, let's call it codeProj. We are going to create 2 orphan branches for our documentation. One is for staging the documentation (this will be pushed from the base documentation repository). The other, gh-pages, will be for production documentation that pulls in staging when there are updates (this avoids overwriting any customizations made).

```
#Navigate to the directory
cd ~/user/Development/codeProj/

#Create the first orphan branch (staging-gh-pages)
git checkout --orphan staging-gh-pages
#Remove all of the files from master in the branch
git rm --cached -r .
#Create a readme to commit
touch README.md (you can add content to this)
#Add and commit the branch
git add .
git commit -m 'Initial Commit'
#Push the branch
git push origin staging-gh-pages

#Create the second orphan branch (gh-pages)
git checkout --orphan gh-pages
#Remove all of the files from master in the branch
git rm --cached -r .
#Create a readme to commit
touch README.md (you can add content to this)
#Add and commit the branch
git add .
git commit -m 'Initial Commit'
#Push the branch
git push origin gh-pages
```

Next, contact the documentation administrator to push the documentation to your staging-gh-pages branch. You must provide your SSH repository url and your branch must be named staging-gh-pages. Once this is done, you can merge the staging-gh-pages branch into the gh-pages branch. The gh-pages branch is where you make your customizations and staging is just used for receiving base documentation updates.

```
#Get the base documentation from remote
git checkout staging-gh-pages
git pull origin staging-gh-pages --allow-unrelated-histories
#Checkout gh-pages branch
git checkout gh-pages
#Merge the branches
git pull origin staging-gh-pages --allow-unrelated-histories
#Finish the merge
You will need to use console to write and quit the merge docs (press esc and then 'wq!' generally)
```

Next, we customize _config.yml file in the gh-pages branch to make it all work. Use your preferred editor to make modifications. Change all references to "gh-pages-boilerplate" to your project and repository names where needed in the file.

```
#Checkout the gh-pages branch
git checkout gh-pages
vi _config.yml (or use your preferred editor)
#Modify the file
title:  A@A Template Documentation
description: A demo of the template documents
email: 			adobeatadobe@adobe.com
baseurl: 	  "/pages/aaa/gh-pages-boilerplate" # the subpath of your site, e.g. /blog
theme: jekyll-theme-cayman # theme from jekyll github account
google_analytics: [Your Google Analytics tracking ID]
show_downloads: false
github: 
    is_project_page: true
    is_user_page: true
    repository_url: https://git.corp.adobe.com/aaa/**gh-pages-boilerplate**
    repository_name: 'GH Pages Boilerplate'
    owner_url: http://www.adobeatadobe.com
    owner_name: Adobe@Adobe
repository: aaa/gh-pages-boilerplate # location of your repository
markdown: kramdown # markdown engine

#Social Media Accounts
twitter_username: adobeatadobe
github_username: aaa
youtube_username: adobeatadobe
behance_username: adobeatadobe
wordpress_username: aaa
#Add and commit the changes
git add .
git commit -m 'Setting up the config file'
#Push the docs
git push origin gh-pages
```

Finally, we go into Github and the code repository settings. In there, you will find an option for Github Pages Source. Set this to the 'gh-pages branch' option in the dropdown menu. If it's working correctly there will be a green bar in the top of this section providing a url to your new documentation. If the css looks off this mean you probably missed something in the _config.yml file.
