---
layout: post
title: "Git Quick Start"
date: 2015-07-30 22:26:38
categories: git
---
### Get git 
***
Git is **open source software** (free for any person to use) written by Linus Torvalds who also wrote the linux operating system.	

It is a program for keeping track of changes over time, known in programming as **version control**

For **Windows**, it's recommended to download Github from [windows.github.com](windows.github.com) and use the **git shell** for your terminal. 
For **Mac**, you can also download Github for Mac from [mac.github.com](mac.github.com).	

Refer to [git-scm.com/downloads](git-scm.com/downloads) for more infomation.

### Configure git
***
Once it is installed, open **terminal**. You can verify that it's really there by typing:

{% highlight bash %}
$ git --version
{% endhighlight %}
next, configure git so it knows who to associate your changes to:
	
{% highlight bash %}
$ git config --global user.name "<Your Name>"
$ git config --global user.email "<youremail@example.com>"
{% endhighlight %}
### Authenticate git
***
When you connect to a Github repository from git, you'll need to authenticate with Github using either HTTPS or SSH.

#### Connecting over HTTPS (recommended) ####
You can cache your Github password in Git using a credential helper.


{% highlight bash %}
$ git config --global credential.helper 'cache --timeout=3600'
{% endhighlight %}
#### Connecting over SSH ####
You must generate SSH keys on each computer you use to push or pull from GitHub as follows.

1. check for SSH keys

	
{% highlight bash %}
$ ls -al ~/.ssh
{% endhighlight %}

By default, the filenames of the public keys are one of the following:
* id_rsa.pub
* id_dsa.pub
* id_ecdsa.pub
* id_ed25519.pub
	
If you see an existing public and private key pair listed that you would like to use to connect to Github, you can skip *step 2* and go straight to *step 3*.
2. generate a new SSH key

With Terminal still open, copy and paste the text below. Make sure you substitute in your Github email address.


{% highlight bash %}
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
{% endhighlight %}
It's strongly suggested to keep the default settings as they are, so when you're prompted to input, just press **Enter** to continue.	
At last, your identification has been saved in ~/.ssh/id_rsa and your public key has been saved in ~/.ssh/id_rsa.pub.
	
3. add your key to the ssh-agent
	
Ensure ssh-agent is enabled,
	
	
{% highlight bash %}
$ eval "$(ssh-agent -s)"
{% endhighlight %}
Add your SSH key to the ssh-agent,
	
	
{% highlight bash %}
$ ssh-add ~/.ssh/id_rsa
{% endhighlight %}
4. add your SSH key to your account

Copy your SSH public key to the clipboard. It's important to copy the key exactly without adding newlines or whitespace.	
Add the copied key to Github.
5. test the connection

Open Terminal and enter: 
	
	
{% highlight bash %}
$ ssh -T git@github.com
{% endhighlight %}
type `yes` if you are prompted `Are you sure you want to continue connecting (yes/no)`.
	
	
{% highlight bash %}
Hi username! You've successfully authenticated, but GitHub does not provide shell access.	
{% endhighlight %}
If the **username** in the above message is yours, you've successfully set up you SSH key!
	
### Create a Repository
***
A **repository** is essentially a project. You can imagine it as a project's folder with all the related files inside of it. In fact, that's what it will look like on your computer anyways.	
You tell git what your project is and git will start tracking all of the changes of that folder. Files added or subtracted or even a single letter in a single file changed -- all of it is tracked and time stamped by git.

To make things easier, name your folder what you'd name the project. The following commands will create a new folder and initialize it as a git repository.


{% highlight bash %}
$ mkdir <projectname>
$ cd <projectname>
$ git init
{% endhighlight %}

### Commit to it
***
Now that you've got a repository started, add a file to it.

Create a file named "*README.md*" in the <*projectname*> folder and write something into it.

Next check the **status** of your repository to find out if there have been changes. Below in this terminal, you should still be within your <*projectname*> folder.


{% highlight bash %}
$ git status
{% endhighlight %}
then **add** the file you just created to the files you'd like to **commit** to change.


{% highlight bash %}
$ git add README.md
{% endhighlight %}
Finally, **commit** those changes to the repository's history with a short description of the updates.


{% highlight bash %}
$ git commit -m "<your commit messsage>"
{% endhighlight %}

If you make some changes to *README.md*, say, add another line to it and save.
In  terminal, you can view the **diff**erence between the file now and how it was at your last commit.


{% highlight bash %}
$ git diff
{% endhighlight %}

### Remote Repository
***
The repository you've created so far is just on your computer, which is handy, but makes it pretty hard to share and work with others on. No worries, that's what Github for.

When you put something on Github, that copy lives on one of Github's servers. This makes it a **remote** repository. By **push**ing your **local** changes to it, you keep it up to date.

Others can always get the latest from you project by **pull**ing your changes from the **remote**.

You want to sync your **local** version with one stored on Github.com called the **remote** version. So first create an empty remote repository on Github.com.

* Go to [github.com](github.com), log in, and click the '+' in the top right to create a new repository.
* Give it a name that matches your local repository's name and a short description.
* Make it public
* Don't initialize with a README because we already have one, locally, named *README.md*.
* Leave .gitignore and License on 'none'.
* Click create repository!

**Readmes**, **.gitignore** and **Licenses**, these are common files in open source projects.	
A **readme** explains what the project is, how to use it, and often times, how to contribute.	
A **.gitignore** is a list of files/folders that git should not track.
A **license** file is the type of license you put on your project, information on the types is [here](choosealicense.com).


### Connect Local to Remote
***
Now you've got an empty repository started on Github.com. It can be identified by a URL, location of the repository on Github's servers, either `https://github.com/username/projectname.git` or `git@github.com:username/projectname.git`.

Back in Terminal, and inside of the <*projectname*> folder that you initialized as a git repository in the earlier challange. You want to tell git the location of the **remote** version. You can have multiple remotes so each requires a name. For your main one, this is commonly named `origin`.


{% highlight bash %}
$ git remote add origin <URL>
{% endhighlight %}
Your **Local** repository now knows where your **Remote** one named `origin` lives on Github. You can **push**(send) everything you've done locally to Github.

Git has a branching system so that you can work on different parts of a project at different times. By default the first branch is named **master**. When you **push**(and later **pull**) from a project, you tell git the branch name and the name of the remote that it lives on.

In this case, we'll send our branch named *master* to our remote one named *origin*.

{% highlight bash %}
$ git push origin master
{% endhighlight %}

Now go to Github.com and refresh the page of your repository. WOAH! Everything is the same locally and remotely.
