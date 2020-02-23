---
layout: post
title: Remote repositories with GitHub
categories: git
excerpt: "Setup remote repositories with GitHub"
tags:
  - GitHub
  - git
  - remote repository
  - clone
  - fork
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
modified: '2020-02-20 T18:17:25.000Z'
date: '2020-02-20 11:27'
comments: true
share: true
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

## Introduction

This post covers connecting a local _git_ clone to a remote master at [gitHub.com](https://github.com). The post is inspired by the Youtube [Introduction to Git - Remotes](https://www.youtube.com/watch?v=Gg4bLk8cGNo) by David Mahler, and the written post [‘Git’ with the Program: Getting Started with GitHub](https://thenewstack.io/git-with-the-program-getting-started-with-github/).

## Create a GitHub account

[GitHub](https://github.com) is free for private users that are satisfied with public repositories. You just sign up, give your email and once you have confirmed your register via your email, and given answers to some simple questions about experiences and interests, you will land at the page "Create a new repository".

![github-nav-new-repo](../../images/github-nav-new-repo.png){: .pull-right}

If you do not get to the page "Create a new repository", use the navigation menu next to the avatar to select "New Repository" (as shown to the right).

Go ahead and create you first repo, the figure below shows the fields to fill.

<figure>
<img src="../../images/github-create-new-repo-filled.png">
<figcaption> Github - Create a new repository.</figcaption>
</figure>

You have to give the repo a name ("my-first-repo" in the example above). Also fill in a <span class='textbox'>Description</span> and let the repository be _Public_ (to use _Private_ repos comes with a fee). Click the radio button for _Initialize this repository with a README_. Click <span class='button'>Create Repository</span> and behind the scenes GitHub is _staging_ and _commiting_ the README.md file.

![github-dismiss-github-action-popup](../../images/github-dismiss-github-action-popup.png){: .pull-right}

When the repo is ready, GitHub will open a page with your repo. If there is a pop-up window requiring about GitHub Actions (as shown to the right), just click <span class='button'>Dismiss</span>.

Your first GitHub repo is created, including one (1) _commit_ at branch _master_ that locked in the <span class='file'>README.md</span> markdown document. All summarised on the repo page shown below.

<figure>
<img src="../../images/github-my-first-repo-commit01.png">
<figcaption> Github - My first repo with a single commit.</figcaption>
</figure>

## SSH connection

With SSH keys, you can connect to GitHub without supplying your username or password at each visit. Thie section is a summary of GitHub's manual for [Connecting to GitHub with SSH](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh).

### Check for existing SSH keys

First check for any existing SSH keys. As SSH keys are OS dependent, follow the instructions for your OS at [Checking for existing SSH keys](https://help.github.com/en/github/authenticating-to-github/checking-for-existing-ssh-keys).

### Generating a new SSH key and adding it to the ssh-agent

If you do not have an existing SSH key and wish to generate one, follow the GitHub instructions [Generating a new SSH key and adding it to the ssh-agent](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent). The Mac OSX instructions are summarised here. Open a <span class='app'>Terminal</span> and then enter:

<span class='terminal'>$ ssh-keygen \-t rsa \-b 4096 \-C "your_email@example.com"</span>

(ssh-keygen -t rsa -b 4096 -C "thomas.karttur@gmail.com")

(ssh-keygen -t rsa -b 4096 -C "thomas.gumbricht@gmail.com")

```
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/thomasgumbricht/.ssh/id_rsa):
```
```
Created directory '/Users/thomasgumbricht/.ssh'.
Enter passphrase (empty for no passphrase):
```
thelma22
```
Your identification has been saved in /Users/thomasgumbricht/.ssh/id_rsa.
Your public key has been saved in /Users/thomasgumbricht/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:v0J0NJLG8IOGN10bY1tu7wxeGxsLUIA0gObpOIFJKDE thomas.karttur@gmail.com
The key's randomart image is:
+---[RSA 4096]----+
|E.   .o=oo*.o    |
|oo  o. +*+oO     |
|oo o..=.+o+.o    |
|o . oo ....o .   |
|   +   .S.  o =  |
|  o .   .. . * * |
|   .   .  . . *  |
|        .  .     |
|         ..      |
+----[SHA256]-----+

```

<span class='terminal'>$ pico ~/.ssh/config</span>

```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

<span class='terminal'>$ ssh-add -K ~/.ssh/id_rsa</span>

```
Enter passphrase for /Users/thomasgumbricht/.ssh/id_rsa:
Identity added: /Users/thomasgumbricht/.ssh/id_rsa (thomas.karttur@gmail.com)
```

<span class='terminal'>$ ssh-add -K ~/.ssh/id_rsa_karttur</span>

```
Enter passphrase for /Users/thomasgumbricht/.ssh/id_rsa:
Identity added: /Users/thomasgumbricht/.ssh/id_rsa (thomas.karttur@gmail.com)
```

Copy the contents of the id_rsa.pub file to the clipboard:

<span class='terminal'>$ pbcopy < ~/.ssh/id_rsa.pub</span>

<span class='terminal'>$ pbcopy < ~/.ssh/id_rsa_karttur.pub</span>

### GitHub SSH setup

This section describes how to configure your GitHub account to use the SSH key, it is a shortened version of the GitHub page [Adding a new SSH key to your GitHub account](https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account).

![github-menu-select-settings](../../images/github-menu-select-settings.png){: .pull-left}

Go to your GitHub account at [GitHub.com](https://github.com). Click on your avatar, in the drop down menu, select <span class='button'>Settings</span> (shown to the left).

![github-settings-menu-SSH-keys](../../images/github-settings-menu-SSH-keys.png){: .pull-right}

<br />
<br />
<br />

In the user settings window that opens, look at the sidebar for <span class='button'>SSH and GPG keys</span> (as shown to the right), and click it.

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

In the page for SSH-keys and GPG-keys that opens, click the <span class='button'>New SSH key</span> button (below).

<figure>
<img src="../../images/github-SSH-keys-page.png">
<figcaption> Github - SSH keys page.</figcaption>
</figure>

A new page, "SSH keys / Add new", opens (below),
In the <span class='textbox'>Title</span> field, add a descriptive label for the new key. The title should reflect both the machine (owner) and the lock (the GitHub repo). Then paste the content of the clipboard, captured with the <span class='terminalapp'>pbcopy</span> command, in the <span class='textbox'>Key</span> field. When done, click <span class='button'>Add SSH key</span>.

<figure>
<img src="../../images/github-Add-SSH-keys-page.png">
<figcaption> Github - add a New SSH key.</figcaption>
</figure>

![github-add-SSH-key.confirm-pswd](../../images/github-add-SSH-key.confirm-pswd.png){: .pull-right}

If prompted to confirm with your GitHub password, do that.

You should now have the same SSH key defined in your machine and on GitHub. And be ready for seamlessly linking your remote and local _git_ repos.

<figure>
<img src="../../images/github-list-of-SSH-keys.png">
<figcaption> Github - list of SSH keys.</figcaption>
</figure>

## Grab the SSH for a repo

Return to the [GitHub](https://github.com) page with the repo ("my-first-repo") that you created above. Towards the right side, approximately mid down there is a <span class='button'>Clone or Download</span> button (shown below).

<figure>
<img src="../../images/github-repo-clone-download.png">
<figcaption> Github - Repository clone or download potions.</figcaption>
</figure>

![github-repo-clone-download-set-SSH](../../images/github-repo-clone-download-set-SSH.png){: .pull-right}

Click on the <span class='button'>Clone or Download</span> button, the default is **Clone with HTTPS** (shown in thus full view figure above), if you click the smaller text "Use SSH" the setting will change to **Clone with SSH** (shown to the right). Do that. And then copy the string in the textbox starting with <span class='textbox'>git@github.com...</span>. This string will allow us to connect from a local _git_ repo directly to the remote repo on GitHub.

## Clone to local repo

Open a <span class='app'>Terminal</span> window and <span class='terminalapp'>cd</span> to the parent directory where you want to create the _clone_ of your remote (GitHub) repository. Then enter:

<span class='terminal'>$ git clone </span>

If you followed the instuctions in the previous section, you can now just paste the SSH link from your clipboard to the command line:

<span class='terminal'>$ git clone git@github.com:thomasgumbricht/my-first-repo.git</span>

Execute the command and your remote rep ("my-first-repo") should clone to your local machine. If this is the first time you use the SSH key, you will be prompted the following statement and question:
```
Cloning into 'my-first-repo'...
The authenticity of host 'github.com (140.82.118.4)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)?
```

Answer with a full <span class='terminal'>yes</span>

```
Warning: Permanently added 'github.com,140.82.118.4' (RSA) to the list of known hosts.
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
Receiving objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
```

### Local repo settings

The [first post of this series](../blog-git-local-use) explains how to [Check and setup user name](../blog-git-local-use). For the cloned repo ("my-first-repo") you can setup a local user and email that matches the SSH key. First <span class='terminalapp'>cd</span> to the clone of the repo, and then set user and email:

<span class='terminal'>$ cd my-first-repo<br>$ git config --local user.name thomasgumbricht<br>$ git config --local user.email thomas.karttur@gmail.com</span>

### git remotes

The command <span class='terminalapp'>git remote</span> returns the remotes for the repo. With the terminal window still point to the cloned repo ("my-first-repo"), type:

<span class='terminal'>git remote</span>

```
origin
```

The name _origin_ is like a _git_ alias for the default remote repository. To see the full paths (urls) and the rights that we have for remotes, type:

<span class='terminal'>git remote -v</span>

```
origin	git@github.com:thomasgumbricht/my-first-repo.git (fetch)
origin	git@github.com:thomasgumbricht/my-first-repo.git (push)
```

### git log

In the post on [git branches](../blog-git-branches) the following command was introduced as a means to get a condensed graphical view of the branches and the _commit_ history:

<span class='terminal'>$ git log --all --decorate --oneline --graph</span>

```
* 9f30e5b (HEAD -> master, origin/master, origin/HEAD) Initial commit
```

For the _clone_ we are working with the _HEAD_ pointer points towards two new items: _origin/master_ and _origin/HEAD_. As _origin_ can be seen as an alias for the primary remote repo, the pointing is towards the reomte (GitHub) repo. As _HEAD_ is pointing both towards the local _master_ and the remote _master_, our local repo is in sync with the GitHub repo.

### Edit origin/master

to try the different functions for linking a remote and a local repositories, return to your [online GitHub account](https://github.com) and the _origin/master_ repo ("my-first-repo"). When in that repo, click the <span class='button'>Create new file</span> button.

<figure>
<img src="../../images/github-create-new-file-click.png">
<figcaption> Github - click the Create new file button.</figcaption>
</figure>

In the window that opens, give the name of the new document in the textbox that says <span class='textbox'>Name your file...</span>. Then enter a few lines in the area for <span class='textbox'>Edit new file.</span>.

<figure>
<img src="../../images/github-create-new-file-page.png">
<figcaption> Github - Create new file.</figcaption>
</figure>

When done, scroll down towards the bottom of the page, GitHub has created a default (short) message. If you accept that message just click the <span class='button'>Commit new file</span> button.

<figure>
<img src="../../images/github-create-new-file-commit.png">
<figcaption> Github - Commit new file.</figcaption>
</figure>

The edits you made are _staged_ and _commited_ by GitHub, and you are returned to the front page of your online repo. If you look, it now says you have two commits, and in the list of contents you can see two files, each with its own _commit_.

<figure>
<img src="../../images/github-my-first-repo-commit02.png">
<figcaption> Github - My first repo with two commits.</figcaption>
</figure>

### git fetch

Return to the <span class='app'>Terminal</span> window that points to your local clone of the GitHub (remote) repo. Your local copy should now be behind the online  (_orign/master_). However, your local _git_ is not yet aware of the latest online _commit_. You can check that out by either <span class='terminalapp'>git status</span> or <span class='terminalapp'>git log</span>. For your local _git_ clone to catch up with online changes, you need to run <span class='terminalapp'>git fetch</span>.

<span class='terminal'>$ git fetch</span>
or
<span class='terminal'>$ git fetch origin</span>

```
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:thomasgumbricht/my-first-repo
   9f30e5b..9cd2c08  master     -> origin/master
```

Check the status of your local repo:

<span class='terminal'>$ git status</span>

```
On branch master
Your branch is behind 'origin/master' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean
```

You can explore the situation graphically:

<span class='terminal'>$ git log --all --decorate --oneline --graph</span>

```
* 9cd2c08 (origin/master, origin/HEAD) Create Chapters.md
* 9f30e5b (HEAD -> master) Initial commit
```

The local _master_ is trailing _origin/master_.

### git merge

The post on [git branches in local repositories](../blog-git-branches) outlined how to use <span class='terminalapp'>git merge</span>. As you have not done any edits to your local (receiving) repo, the _merge_ of the _origin/master_ can be done as a fast-forward _merge_ (straight update of the _HEAD_ pointer to the latest _commit_):

<span class='terminal'>$ git merge origin/master</span>

```
Updating 9f30e5b..9cd2c08
Fast-forward
 Chapters.md | 5 +++++
 1 file changed, 5 insertions(+)
 create mode 100644 Chapters.md
```

You can check that your local clone is in sync with _orgin/master_ by either <span class='terminalapp'>git status</span> or <span class='terminalapp'>git log</span>.

<button id= "toggleStatus01" onclick="hiddencode('Status01')">Hide/Show git status response</button>

<div id="Status01" style="display:none">

{% capture text-capture %}
{% raw %}
```
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

<button id= "toggleLog01" onclick="hiddencode('Log01')">Hide/Show git log --all --decorate --oneline --graph response</button>

<div id="Log01" style="display:none">

{% capture text-capture %}
{% raw %}
```
* 9cd2c08 (HEAD -> master, origin/master, origin/HEAD) Create Chapters.md
* 9f30e5b Initial commit
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

### git pull

The <span class='terminalapp'>git pull</span> command combines <span class='terminalapp'>git fetch</span> and <span class='terminalapp'>git merge</span> into a single command. Both online [GithHub](https://github.com) repos and the [<span class='app'>Github Desktop</span> app](https://desktop.github.com) have predefined functions for _pull_ (rather than _fetch_ + _merge_). It is, nevertheless, often better to use _fetch_ + _merge_.

### git push

The command <span class='terminalapp'>git push</span> is used for sending local clone changes to remote repos. To test it, make some edits to the local copy of <span class='file'>Chapters.md</span>. You can use any editor, for instance <span class='terminalapp'>pico</span>:

<span class='terminal'>$ pico Chapters.md</span>

```
...
## Add another chapter
```

Hit [ctrl]+[X] to exit <span class='terminalapp'>pico</span> and save the edits by pressing <span class='terminal'>Y</span> when asked.

_commit_ the changes with the combined command:

<span class='terminal'>$ git commit -am "Added chapter to Chapters.md"</span>

```
[master 0b4547f] Added chapter to Chapters.md
 1 file changed, 2 insertions(+)
```

<button id= "toggleStatus02" onclick="hiddencode('Status02')">Hide/Show git status response</button>

<div id="Status02" style="display:none">

{% capture text-capture %}
{% raw %}
```
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

<button id= "toggleLog02" onclick="hiddencode('Log02')">Hide/Show git log --all --decorate --oneline --graph response</button>

<div id="Log02" style="display:none">

{% capture text-capture %}
{% raw %}
```
* 0b4547f (HEAD -> master) Added chapter to Chapters.md
* 9cd2c08 (origin/master, origin/HEAD) Create Chapters.md
* 9f30e5b Initial commit
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

The local clone of the repo is now 1 _commit_ ahead of _origin/master_. To put them in sync again, <span class='terminalapp'>git push</span> the local changes to the remote repo:

<span class='terminal'>$ git push origin master</span>

```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 339 bytes | 169.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:thomasgumbricht/my-first-repo.git
   9cd2c08..0b4547f  master -> master
```

<button id= "toggleStatus03" onclick="hiddencode('Status03')">Hide/Show git status response</button>

<div id="Status03" style="display:none">

{% capture text-capture %}
{% raw %}
```
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

<button id= "toggleLog03" onclick="hiddencode('Log03')">Hide/Show git log --all --decorate --oneline --graph response</button>

<div id="Log03" style="display:none">

{% capture text-capture %}
{% raw %}
```
* 0b4547f (HEAD -> master, origin/master, origin/HEAD) Added chapter to Chapters.md
* 9cd2c08 Create Chapters.md
* 9f30e5b Initial commit
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

A quick look at your [GitHub online](https://github.com) repo (remember to refresh the page) reveals that you have now three commits, with the latest message being "Added chapter to Chapters.md".

<figure>
<img src="../../images/github-my-first-repo-commit03.png">
<figcaption> Github - My first repo with three commits.</figcaption>
</figure>
