---
layout: plain
---


# Jekyll How To Create a free website on Github using openSUSE
openSUSE specific steps<br />
Based on the documentation at http://jekyllrb.com

## Preamble:
This documentation is written to avoid faulty mis-steps like the overly brief and insufficient documentation elsewhere, including http://jekyllbootstrap.com/

This document was created following the steps described here, and was used as the initial testbed for this Guide. A curious person can clone this website and inspect everything about it, including the markdown syntax used.

## Caution:
These steps and the resulting Ruby on Rails environment is very openSUSE specific. If this is only your website or other team members are all using openSUSE, then these steps are fine. But, if you intend to set up a website supported by multiple team members using different Linux distros (or even Windows) then wait for a follow up article which will describe building a common Development environment for all.

## Why and what is Jekyll?
Jekyll is the current fully supported JS static website framework supported by Github.<br />
Github will serve all content including websites based entirely on publicly viewable code for free, no strings attached (except as of this writing file size).<br />
Free is good.<br />
Extreme stability and reliability plus unlimited storage for Free is even better.

## Preparation:
You should first decide where you will want to create your local instance of your website. There is no right or wrong place to do so and since you will use a JS webserver (optionally included in Jekyll), you do not have to install a big webserver which would have fixed required locations.
If the website will be yours alone, you might plan on a location in your Home directory, maybe a subdirectory of your Documents folder.
If your website will be shared with others through Github, you will more likely prefer creatinga a centralized "parent" github folder somewhere and create the repo containing your Jekyll website as a subdirectory.

These instructions will be based on the last suggested above configuration, that you intend to deploy your Jekyll website on Github and will contain appropriate recommendations.

## Prerequisites:
Ruby =>2.0
Linux (in general, although there are special instructions to install on Windows)

### Installing Ruby:
. openSUSE is different than other distros. Many distros fully provide all libraries in their main repositories, but openSUSE is not one of them. Although basic Ruby functionality is provided in the main repo, you need to install the special Ruby repo if you intend to install and benefit from latest stable additions and versions. On openSUSE you can install the Ruby repo as follows(modify openSUSE version if different). For any other distros, research a bit to determine what you may need to do (or not).

```zypper ar http://download.opensuse.org/repositories/devel:/languages:/ruby:/extensions/openSUSE_13.2/ devel:languages:ruby:extensions && zypper ref```

install Ruby at least version 2.0, development header and libraries, support for the ruby "gems" command, the ruby version manager(RVM). On openSUSE, the following and an appropriate javascript runtime... The following installs the most current widely used version of Ruby as of this writing  plus nodejs which is an excellent cross-platform js runtime.

``` zypper in ruby ruby2.1 ruby2.1-devel rubygem-rubygems-update rubygem-bundler nodejs ```

## Installing Jekyll
Cool! - After installing the prerequisites described above, you are now ready to install Jekyll not from your ordinary repositories but from the official Ruby repositories. Invoke the following

``` gem install jekyll ```

You are now done installing, now on to creating a website!





## Creating a Jekyll static website

The following describes creating a bootstrap website which means a fully functional starting point with a sample index.html and supporting folder structure, scripts and files.

Although for a personal website you can create one anywhere on your machine, the following specifically recommends an approach for creating a website for deployment on Github.

### Decide, and designate a location for your Github projects
Create a directory for all your github projects.I arbitrarily recommend a subdirectory of the current User Home directory, ie /home/username/ This folder can be created with the following command from a console app of your choice (Some popular console apps include BASH, Konsole, xconsole, )

``` mkdir ~/github ```

Now, let us move your command line console to the directory you just created

``` cd ~/github ```

### Create a repository on Github
Setting that console aside for a moment, the next step is to create a repository on github, then create a local linked copy in this directory you just created. Although it is possible to create a new repo on github from your console, it is far easier and simpler to use a web browser.

Open your web browser to "https://github.com/accountname" The accountname would generally be either your own account handle/nickname or an organization handle/nickname.

Verify your web browser is already logged into your account, in the bar running across the top of the page, to the right should display your name, a big "plus", a notifications(picture) icon, a settings icon, and a "sign out" icon. If your name is not displayed, login.

After you have logged into github and your name is now showing, click on the big "plus" icon and select "New repository." If you are connecting to an organization, a repo may have already been created and you can skip this and the next couple steps to "Clone the repo on Github to your local machine"

The "Create Repository" page should now display, enter the name of the repo you wish to create and an optional description. Leave the Public/Private setting to Public, only public repos which can be viewed by everybody are free. Later if you wish, you can pay to create a private repo.  Do check the box "Initialize this repository with a README" -- This automatically configures some settings whether you intend to keep this file or not.

Click the button "Create repository" to finish.<br />
Although Github says it can take minutes to create your repository, I have always seen github perform all tasks instantly (at most few seconds, shorter than it might take to switch to another app).

### Clone the repo on Github to your local machine<br />
Whether someone created a repo on Github for you or you just created your new repo, you are now ready to create a local working copy of the remote repo on your machine, and  "push" your own modifications to Github.

First, using your web browser, browse to the web page for your new repo. The breadcrumb on the webpage just below the bar at the top of the page should display your handle or nickname, slash reponame

In the right pane on this page, you should see "HTTPS" over a URL and "Download ZIP" Copy the URL into memory (aka clipboard). The ZIP might be a convenience for anyone who simply wants a one time download and doesn't want an interactive copy of the files in the repo.

From your console, if it is not already at ~/github/ or a similar location according to your own organizational senses...

Enter the following into your console which is the command to "git clone _youruri_" .<br />
``` git clone [paste] ``` followed by "enter"


On some distros, you might not be able to paste from the clipboard into your console. If this is your situation, simply paste the clipboard contents into your GUI text editor so you can see the entire URL and manually enter the above command into your console.

The "clone" command will<br />
- Automatically create a new subdirectory using the repo name<br />
- Copy the file contents of the repo on Github into your subdirectory with the repo name.

### Installing a new Jekyll bootstrap website<br />
This section is only for those who are creating something absolutely, really, really new and is unnecessary for anyone who has cloned an existing website. If you are simply collaborating on an existing website, you can skip the following steps which create a website and skip down to the section invoking an existing website (assumes you have performed the above, installing Jekyll prerequisites on your machine).

Typically, your console app should currently be in ~/github/. You can ls to verify your cloned repo directory exists

``` ls ```

Change directory your console to the root of your repo (not the github repo where you likely are).

``` cd ```_directoryname_

You can ls again and find only one file "README.md" If you do not find a README.md, then you missed creating it as part of the repo creation. Although it is possible to manually finish the repo setup, for a beginner it is probably easier to delete the local repo and the Github repo, and create the Github repo again (with the README.md)

``` ls ```

Now that you have a local copy of your nearly empty repo ready, we will now populate it with a Jekyll bootstrap website (beginning, functional website).

**IMPORTANT NOTE:** <br />
The Reader will find it is noteworthy you can add (create new or copy from elsewhere) files into your local repo, but once you have pushed your copy to Github effectively synchronizing both a copy on Github with your local copy, you cannot simply delete or remove a file using ordinary means. You would have to use the git command "git rm _filename_" to remove any files to ensure the removal is logged so it is also performed on the remote server.

### Switching from the "main" to "gh-pages" branch<br />
The Main branch of a github repo simply stores and serves files like an ordinary file server. If you want your files deployed by the github webserver, you need to deploy your files to the "gh-pages" branch and not the "main" branch.

The previous instructions to this point have described  how to create a repository on Github.com and clone a local copy on your machine, but by default it will sync only the main branch. We need to change from the main branch to the gh-pages branch for github webserver functionality.

The following steps are what is described in the official "github creating gh-pages manually" https://help.github.com/articles/creating-project-pages-manually/

If your console isn't already at the root of your local, cloned repo.<br />

``` cd ``` **repository**

``` git checkout --orphan gh-pages ```<br />
# Creates our branch, without any parents (it is an orphan!)<br />
# Switched to a new branch 'gh-pages'


Although you've switched to gh-pages, your local repo copy is still populated with the files in the main branch. You need to remove those files with the following commands (note using the "git rm" command because the ordinary "rm" command is insufficient)<br />

``` git rm -rf .```<br />
# Remove all files from the old working tree. Notice hard to see "." designating "any/all files"
rm '.gitignore'

Now that your repo is connected to the gh-pages branch and is completely empty, you can install your Jekyll bootstrap(a functional minimal website with full file layout and scripting support)

**NOTE:** On openSUSE and possibly other distros, different versions of jekyll may be installed. If the "jekyll" command does not work immediately, then the binary name may have been modified to reflect the version. To determine the binary name, run the following command and use the result in place of the generic "jekyll" from now forward.

``` ls /usr/bin/jekyll* ```

Now install the jekyll bootstrap (use whatever is appropriate in place of "jekyll" if needed)

``` jekyll new . ```

Now, if you wish you can immediately test your work by invoking the jekyll embedded webserver with the following command. After a few seconds auto-generating some default config files, the stdout will report "Server running... press ctrl-c to stop." When that displays, open a web browser to "http://localhost:4000"

```jekyllserve ```


# Pushing to github.com
You have tested your website by running a small, non-production test webserver locally, you can now push it to github for the world to see... Perform the following "Required" steps for uploading to github (other commands are listed here which may be helpful).

## The basic steps for interacting with a github repository
For most people, if you never are never in a position to manage a github repo... merging, rollback, managing different branches and resolving inconsistencies the following 5 git commands may be all you'll ever use.


### (optional) Lost track what what you have done?<br />
Have your changes been committed? Anything else that is missing before your next step? "Status" displays pending changes and proposes a logical next step <br />
``` git status ```

### (optional) "Pull"<br />
If you believe the remote repo at github.com might have been modified since you last created or updated your local copy. This "pulls" any changes so you are up to date. Essential to minimize later "merge" inconsistencies. <br />
``` git pull ```

### (Only once, never again) Create initial local copy <br />
``` git clone *reponame* ```

## (Required, uploading)<br />
You have made your proposed changes, now you need to "commit" your changes with a descriptive comment about your changes <br />
``` git commit -am "comment" ```

## (Required, uploading)<br />
You have committed your proposed changes and certain about offering your changes to your Collaborators. Let us "push" your changes to Github.com. If you are missing any global configurations, you will be prompted to fix. When prompted, enter Username and Password. <br />
``` git push ```

You should now be able to view your website on github using the following URL (modify accordingly)

``` https://```**_Username_**```.github.io/```**_reponame_** 


## Some useful references:

### Github flavored Markdown
Now that you have your bootstrap deployed to Github, you can modify pages however you wish on your local copy, then pushed to Github. But whether you are familiar with HTML or not, what is this Markdown? It is a faster alternative to HTML, although you can use HTML this is your reference to using Markdown on Github<br />
https://help.github.com/articles/github-flavored-markdown<br />
A popular Cheatsheet to keep at your elbow<br />
https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

### Some other advanced concepts
Javascript frameworks are great. They are pre-packaged libraries of functionality you can invoke often by command instead of writing all the necessary code yourself.You can either deploy the library files in a subdirectory of your website and reference it in the page <head></head> or you can reference a CDN (Content Delivery Network) in the head so that the Client downloads from there instead.

### Change your look!
Jekyll implements Liquid themes so that you can change the look instantly without affecting the content.

### Some Jekyll Themes (available)
https://github.com/jekyll/jekyll/wiki/Themes
### More Themes
http://jekyllthemes.org/

### Switching from one theme to another, aka Changing your Look
At least one popular Jekyll "How To" site described creating a new site and migrating content to simply change themes, Don't! You can find, browse and install themes using rake<br />
http://jekyllbootstrap.com/usage/jekyll-theming.html















