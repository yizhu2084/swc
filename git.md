# Establishing your online presence with Git and GitHub pages

 - **Author**: Gaurav Kolekar
 - **Lesson Topic**: Git and GitHub
 - **License**: GNU GPLv2
 - Adapted from [Bruno Grande](https://github.com/brunogrande/lesson-github-pages/blob/master/lesson/lesson.md)
 
## Motivation

It is becoming evermore important to establish a web presence, even as an undergraduate student. Facebook, Twitter, and the like are methods for doing this, but many would agree that it is much more professional to give people a snazzy website. Historically, people gravitated towards large website creation websites or had to learn HTML and other languages to build their own websites. Then there was the arduous task of finding or paying someone to host your website. Fortunately, the increased expectation of creating and maintaining a website is correlated with the increased ease in doing so, due in part to cloud-based hosting solutions and intuitive markdown-based methods of building content.

GitHub has emerged as one of the best options creating an awesome looking website easily and cheaply (even free!). As the name implies, GitHub was founded as simply a online hub, or hosting service, for Gits, or as they are commonly called, Git repositories. Git, put simply, is a flexible and powerful file management and archival system. It was built with complex project management in mind, in an effort allow project developers to keep track of file identities and versions, and seamlessly navigate through this complex temporal and hierarchical file-system structures. If this isn't making sense, the comic below more-or-less outlines what Git allows users to avoid.

## Overview of Lesson

Learners will complete the following broad tasks:

1. Fork a website template repository on GitHub and use Git locally to pull this repository onto their computer.

2. Make necessary changes to setup the website and then add content, using Markdown, while learning the basics of Git.

3. Push local changes back to remote repository at GitHub, which then automatically builds and displays the website.

4. Users will conclude by populating their website with all materials and overviews of the lessons for the Software Carpentry workshop they participated in. This will allow them to reference this information later.

## Forking and Cloning a Repository

GitHub Pages, GitHub's service that builds and hosts websites, utilizes several fairly complex programming languages, thus saving the user the trouble of knowing them in great depth. One simply has to provide a properly formatted repository and GitHub does the rest. We will take advantage of this, plus open source website templates, to create personal websites. For this lesson, learners will be using the [Jekyll Now template]
(https://github.com/barryclark/jekyll-now), but there are [many options]
(http://jekyllthemes.org/) out there.

This template is contained in a repository owned by [Barry Clark]
(https://github.com/barryclark), so we cannot edit it ourselves. Rather, we will be creating our own copy of it and then modifying it to our liking. The copying will take place on GitHub using a process called 'forking' and the editing will take place using a simple text editor on the user's local computer. Visit the Jekyll Now template repository and click the Fork button at the top-right. If you happen to already be affiliated with another organization in GitHub, you may be prompted to select an account, and you should use your personal GitHub account.

We'll make some pretty basic changes online to the repository settings. Under the top tabs is a brief description of the repository that we inherited as part of this template. Click to edit and give your repository a new, brief description. Also include the URL we will use to access your forthcoming website, which should be `<username>.github.io`, where `<username>` reflects your GitHub username.

From here, we will work further on our repository on our local computer. To do so, we must download the repository from GitHub, which is called 'cloning'. We can do this as a zipped file, but let's instead learn our first bit of Git. Along the top of your files list you should see a URL. Be sure that the box to the left reads 'HTTPS' and not 'SSH'. The latter requires some further steps, that we will leave that for you to do later using instructions on [setting up SSH keys]
(https://help.github.com/articles/generating-ssh-keys/). Copy the HTTPS link and in your Terminal type the following commands:

```bash
# Create a 'Repos' directory in your $HOME folder
mkdir -p ~/Repos
# Change into your new directory
cd ~/Repos
# Clone your website template repository from GitHub
git clone https://github.com/<username>/<username>.github.io.git
```

You should now see a see a local copy of your repository in the working directory.

## Exploring Git

We should now spend some time explaining Git in more detail.

```bash
# Change into your repository directory and view its contents
cd <username>.github.io
ls
```

You should see the same exact list of files that was observed on GitHub. So what makes this a Git repository? It appears to be like any other directory. Let's explore that question.

```bash
# List the full contents of the directory, including hidden files, as a single column
ls -1a
.
..
.git
.gitignore
404.md
```

You should now notice several files with leading dots, indicating they are hidden. The first and second represent the working and upper-level directories, respectively. The next '.git' file is the key to a Git repository, as it contains the information that Git (and GitHub, which is essentially Git running on a server, with some fancy add-ons) use to manage this directory as a repository.

We've copied this directory, so let's take a quick tangent and explain how one would initialize a Git repository in any directory.

```bash
# Change directory to the upper-level (notice the use of the ..)
cd ..
# Make a new directory called whatever you want (I'm using 'biology') and move into it
mkdir biology
cd biology
# Create some empty files/directories to make this appear like a normal directory
mkdir genetics ecology microbiology
touch zoology botany
```

So now we have essentially the same thing as our copied website template, but without the 'fancy' Git hidden files. Let's create those now.

```bash
# Initialize your directory as a Git repository
git init
# View the directory contents
ls -1a
.
..
.git
botany
```

So we now have the the .git hidden file, but what about that .gitignore one. All the .gitignore file specifies are the files and/or directories that you want Git to ignore when it tracks the files in your repository. Therefore, if we find plants boring (because they are!), we could have Git ignore the 'botany' file. We do this by simply adding the names of the files/directories we want to ignore.

```bash
# One way of adding 'botany' to our gitignore, sans text editor
echo 'botany' > .gitignore
```

That gives some basic Git information, and we'll explore more with real files inside of our website repository.

## Setting Up Your Website

We'll begin by configuring a couple files that establish the overall website design and that tell our visitors some basic information about ourselves. Let's first edit the _config.yml file to set some overall design parameters. Open this file in a text editor and fill in some basic information.

```
name: <name>
description: <name>'s website
url: <username>.github.io
```

Let's also replace that stock photo with something more personal. Go online and find a picture of yourself, or of something fitting of yourself (that you have permission to use). In many cases, you can right-click and select "Copy Image URL" or something similar. If your lazy you can just use your GitHub image. You can place this as your avatar.

```
avatar: http://domain.extension/images/picture.jpg
```

Now let's edit the 'About' page on our website and provide any visitors with basic information about yourself. When you open the file in a text editor, you'll see the following header. It simply specifies information about the page design, title, and relative link.

```
---
layout: page
title: About
permalink: /about/
---
```

Next you can modify the text accordingly to tell people about yourself. Notice the pound signs at the beginning of a couple lines and how they translate to the relative text rendering on the website. The syntax is called Markdown and it allows us to take simple text and add some flare without a bunch of coding knowledge. This lesson overview is written in markdown as well. You can use the brief guide at GitHub to get a feel for Markdown.

## Integrating Our Changes and Visualizing the Results

Now we want to see what our changes have done to the website. This will introduce the most commonly used Git commands. Let's start by viewing our Git status.

```bash
git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   _config.yml
	modified:   about.md

no changes added to commit (use "git add" and/or "git commit -a")
```

The output provides us with some useful information, like the branch name (something we won't really discuss today). It also includes our two modified files and tells you that neither have been added to commit. Let's progress by both adding and committing the changes we've made. You should also view the Git status after each one.

```bash
git add _config.yml about.md
# Hopefully you are noticing the intuitive verbs that Git uses
# This one adds your files to Git's tracking
git commit -m "added some basic website info"
# This command commits your changes and provides a useful message about what they are
```

You can also view your Git log and see info on the changes you've just made, including obvious things and also a computer generated label for the commit (that long alphanumeric string).

```bash
git log
commit 3868e34b3866853028a2d7af6f6b10977b19d7a4
Author: Gaurav Kolekar <gaurav.kolekar01@gmail.com>
Date:   Sat Oct 15 01:40:05 2016 -0500

    added some basic website info
```

The steps you just took made your first Git commit, so Git has recorded these initial changes. Let's make some more quick changes to your _config.yml. You'll notice that there are fields like 'email' and 'github' (and others) where you can include your email address and GitHub handle for people to interact with you. Fill one or two in. 

Another key attribute of Git is that it allows you to compare versions of files and note differences. Let's compare our _config.yml file from our two commits.

```bash
git diff
diff --git a/_config.yml b/_config.yml
index b89b129..5a4572f 100644
--- a/_config.yml
+++ b/_config.yml
@@ -21,12 +21,12 @@ footer-links:
   email:
   facebook:
   flickr:
-  github:
+  github: darencard
   instagram:
   linkedin:
   pinterest:
   rss: # just type anything here for a working RSS icon
-  twitter:
+  twitter: darencard
   stackoverflow: # your stackoverflow profile, e.g. "users/50476/bart-kiers"
   youtube: # channel/<your_long_string> or user/<user-name>
   googleplus: # anything in your profile username that comes after plus.google.com/
```

As you can see, Git gives you pretty intuitive information on the files being compared (plus abbreviated labels) and the specific changes made to the file. Now go ahead and practice adding and committing your new changes. If you view your log again you'll see this second commit.

Now let's say that you made a mistake in editing the _config.yml file. In this context, it would be very easy to open the file back up and make a couple quick edits. However, what if this file is much more complex, like a long shell script, or what if you go through a series of edits and still have an error, and just want to revert to the last working version you had. Git allows you to do this.

```bash
# Revert to the previous commit
git checkout HEAD~1 _config.yml
# Revert to the commit before the previous commit (or beyond)
git checkout HEAD~2 _config.yml
# Revert to a specific commit using the full commit label
git checkout a69c34a76c0fa85b7ffc86237fb34c8e0f6ae4c3
```

You can use similar relative or absolute commit syntax to compare committed files using a command we've already seen.

```bash
# Compare two previous commits
git diff HEAD~1 HEAD~2 _config.yml
# Compare our newly edited, uncommited files to an exact commit by label
git diff a69c34a76c0fa85b7ffc86237fb34c8e0f6ae4c3
```

## Integrating Our Changes with our Website

These previous steps demonstrate the basics of Git, which can be used locally to keep track of changes to files without having to make separate file copies for each change. Let's take this full circle and reintegrate our changes remotely, on GitHub's servers, and thus customize our website.

```bash
# Let's make sure we are at the head of our branch
git checkout HEAD
# Push our changes to GitHub where it can be integrated into our website
# 'origin' refers to the remote server and 'master' to the branch
git push origin master
Counting objects: 7, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (7/7), done.
Writing objects: 100% (7/7), 585 bytes | 0 bytes/s, done.
Total 7 (delta 5), reused 0 (delta 0)
To https://github.com/gauravkolekar/scw.git
   050d8a7..b3f97a3  master -> master
```

Now if we refresh our GitHub repository page we should see the changes, including the commit messages. You can click on these files and view their contents, and you can even compare versions within GitHub, just like we've already done locally. Now view your website using your URL and you'll see the changes reflected (sometimes GitHub takes a few minutes to render changes).

## Populating Your Website with Workshop Content

