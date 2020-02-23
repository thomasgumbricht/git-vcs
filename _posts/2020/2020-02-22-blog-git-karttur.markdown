---
layout: post
title: Karttur's git repos
categories: git
excerpt: "Managing Karttur's git repos"
tags:
  - GitHub
  - git
  - remote repository
  - clone
  - fork
  - karttur
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
modified: '2020-02-22 T18:17:25.000Z'
date: '2020-02-22 11:27'
comments: true
share: true
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

## Introduction


### SSH keys

[Dual SSH  keys](https://gist.github.com/jexchan/2351996)


### Creating a new GitHub repo

If I have understood correctly, you can only create an online GitHub repo using a browser and being logged in to your GitHub account. Explained in the GitHub page on [Creating a new repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-new-repository). However, you only need to create the repo, everything else can be done from your local command line as outlined on another of GitHub´s help pages [Adding an existing project to GitHub using the command line](https://help.github.com/en/github/importing-your-projects-to-github/adding-an-existing-project-to-github-using-the-command-line).



### Creating a new gh-pages blog repo

To be completed

### Fork Karttur geoimagine

To contribute towards Karttur's GeoImagine Framework you have to sign up with [GitHub.com](https://github.com) - see the post on [Remote repositories with GitHub](../blog-gig-github).

#### Fork indicidual packages

Indicvidual packages are named geoimagine-"package".

##### Identify source repo

<figure>
<img src="../../images/github-karttur-repos.png">
<figcaption> Karttur's repos at GitHub.com.</figcaption>
</figure>

Go to [Karttur's GitHub account](https://github.com/karttur?tab=repositories),
![github-geoimagine-setup_db-search](../../images/github-geoimagine-setup_db-search.png){: .pull-left}
and identify (search in the <span class='textbox'>Find a repository</span>) the repo you want to _fork_. If for instance you want to work with the package on database setup (_setup_db_) you should look for the repo "geoimagine-setup_db".

![github-fork-icon](../../images/giithub-fork-icon.png){: .pull-left}
Click on the fork symbol to retrieve (_fork_) the repo to your account.

<figure>
<img src="../../images/github-karttur-fork-master-branch.png">
<figcaption> Github - the master branch of the forked project.</figcaption>
</figure>

##### Clone to local machine

To work with the package/repp you need to clone or download. The most difficult way to get the package to your local machine is to clone it with an SSH key (hidden credentials that allows you to seamlessly interact with from your local machine with your online GitHub account) or using [GitHub Desktop](). You can also download, but as you will have to _push any_ changes to you GitHub account to particiapte in teh develoment, that is nto receommendd.

###### Clone using terminal

Open a <span class='app'>terminal</span> window and change directory (<span class='terminalapp'>cd</span>) to the parent folder where you want to have the clone of GeoImagine package. You need to consider the setup of your PyDev Integrated Development Environment (IDE). And locate the package/repo inside your IDE working directory setup for Karttur's GeoImagine Framework.

<span class='terminal'>$ cd /path/to/IDE/workingarea</span>

While the onlne repo has the prefix "geoimagine" you shoudl remove that for the local clone. That is simply done using the standard clone command <span class='terminalapp'>git clone [source-url] [target-name]</span>.

<span class='terminal'>$ git clone git@github.com:thomasgumbricht/geoimagine-setup_db.git setup_db </span>

```
Cloning into 'setup_db'...
remote: Enumerating objects: 10, done.
remote: Counting objects: 100% (10/10), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 124 (delta 2), reused 4 (delta 0), pack-reused 114
Receiving objects: 100% (124/124), 65.10 KiB | 653.00 KiB/s, done.
Resolving deltas: 100% (66/66), done.
```

<span class='terminalapp'>cd</span> to the _cloned_ package/repo/directory and list (ls) the content:

<span class='terminal'>$ cd setup_db<br>$ ls</span>

```
README.md		doc			setup_db_main.py
__init__.py		setup_db_class.py	version.py
```

###### Create development branch

As a developer wanting to contribute, I suggest that you create a _branch_ called _dev_ and then use that for _staging_ and _committing_ edits to the codes and documents.

Working with branches is explored in detail in the post [git branches in local repositories](../blog-git-branches), expanded for use with GitHub in [Remote repositories with GitHub](../blog-git-github) and also how to use with forks in [Forking repositories](../blog-git-forks).

With the <span class='app'>Terminal</span> window still in your local repository ("setup_db"), type:

<span class='terminal'>$ git branch</span>

```
* master
```

There is only one branch in your repo - _master_.

Create a new branch and immediately switch to this branch:
<span class='terminal'>$ git checkout -b dev</span>

 ```
Switched to a new branch 'dev'
```

###### Make some edits

to start the newly created development branch you need to make at least a minor edit to one of the included files. Changing a text string in <span class='file'>README.md</span> is sufficient.

<span class='terminal'>$ pico README.md</span>

```
# geoimagine-setup_db

%%%% Edits added by "githubuser" marked by "%%"  %%%%
```

###### Stage and commit changes

With edits done to the source files you can _stage_ (add) and _commit_ (lock in and save) the changes to your local git repository:

<span class='terminal'>git add .</span>
<span class='terminal'>git commit -m 'edits to README.md'</span>

If you did not create a new file, you can add (-a) the _staging_ to the _commit_ command, and insted of two commands just execute the one:

<span class='terminal'>git commit -am 'edits to README.md'</span>

You can check out is anything is pending in the active branch (_dev_):

<span class='terminal'>$ git status</span>

```
On branch dev
nothing to commit, working tree clean
```

To get a graphical view of the _commit_ log:

<span class='terminal'>$ git log --all --decorate --oneline --graph</span>

```
* a4efe67 (HEAD -> dev) edits to README.md
*   217a091 (origin/master, origin/HEAD, master) Merge pull request #1 from karttur/setup_db_main-edits
```

From the returned message you can see that the local _HEAD_ pointer is ahead of _origin/master_, _origin/HEAD_, _master_, where _origin_ is the default alias for the primary remote repository.

###### Push

Confirm the remote connections of the cloned repo you are working with:

<span class='terminal'>$ git remote -v</span>

```
origin	git@github.com:thomasgumbricht/geoimagine-setup_db.git (fetch)
origin	git@github.com:thomasgumbricht/geoimagine-setup_db.git (push)
```

To send your local changes to your GitHub online account, use the <span class='terminalapp'>git push</span> command:

<span class='terminal'>$ git push -u origin dev</span>

```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 342 bytes | 342.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
remote:
remote: Create a pull request for 'dev' on GitHub by visiting:
remote:      https://github.com/thomasgumbricht/geoimagine-setup_db/pull/new/dev
remote:
To github.com:thomasgumbricht/geoimagine-setup_db.git
 * [new branch]      dev -> dev
Branch 'dev' set up to track remote branch 'dev' from 'origin'.
```

If you execute the extended <span class='terminalapp'>log</span>, you will see that the branch _origin/dev_ has been added, and is up to date with the local _dev_ branch.

<span class='terminal'>$ git log --all --decorate --oneline --graph</span>

```
* a4efe67 (HEAD -> dev, origin/dev) edits to README.md
*   217a091 (origin/master, origin/HEAD, master) Merge pull request #1 from karttur/setup_db_main-edits
```

![github-branch-button-menu-dev](../../images/github-branch-button-menu-dev.png){: .pull-right}

Return to your browser and your online GitHub account with the _fork_ of "geoimagine-setup_db". There should now be one additional branch. If you click on the button <span class='button'>Branch: master</span> a dropdown menu shows all the branches (and some actions you can take).

<figure>
<img src="../../images/github-karttur-fork-dev-branch.png">
<figcaption> Github - the dev branch with your edits of the forked project.</figcaption>
</figure>

###### Review and verify edits

You have made some edits and you want to either merge you edits into you own version of _master_ or submit them to Karttur for updating of the original system (the repo residing with karttur itself). To review and verify edits use the <span class='terminalapp'>git diff</span> command. To find the differences between two branches:

<span class='terminal'>$ git diff master..dev</span>

```
diff --git a/README.md b/README.md
index 85d8158..85e7484 100644
--- a/README.md
+++ b/README.md
@@ -1,5 +1,7 @@
 # geoimagine-setup_db

+%%%% Edits added by "githubuser" marked by "%%"  %%%%
+
 Karttur Geoimagine database setup python project

 ## Introduction
```

As the local clone is in sync with _origin_, the result will be the same if you compare the remote branches:

<span class='terminal'>$ git diff origin/master..origin/dev</span>

If the edits are extensive you can compare difference on a file basis:

<span class='terminal'>$ git diff master..dev -\-\ README.md</span>

###### pull request

At this stage, with reviewed and verified edits that you feel Karttur's GeoImagine Framework would benefit from incorporating, you should create a pull request.

###### git merge
