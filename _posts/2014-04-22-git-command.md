---
layout: post
title: Git Commands - branch, checkout, merge and rebase
description: "Blog post about git commands"
modified: 2014-04-22
tags: git
image:
  feature: abstract-4.jpg
  #credit: dargadgetz
  #creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true
---

## Git branch
Branching is a very useful feature in version control. When a new branch is created, you would have a new working directory, staging area and project history. Commits from the new branch would be recorded in the history of the current branch. The default branch name in Git is `master`. Every time you make a new commit, the `master` moves forward and points to the lastest commit. The illustration below shows that you have make three commits and the 'master' points to the latest commit(C3).
![git_branch_master]({{ site.url }}/images/git_diagrams/git_branch_master.png)

Next, run `git branch experiment`. Running this command will create a new branch called `experiment`. Now, we would have a new pointer that points to the 3rd commit which is the lastest commit that we have.

{% highlight html %}
$ git branch experiment
{% endhighlight %}

![git_branch_experiment]({{ site.url }}/images/git_diagrams/git_branch_experiment.png)

# Git checkout
You may wonder, how would git know which branch you are on and how to switch between branches in Git. Git has a special HEAD pointer that points to the current local branch that you are pointing to.
![git_head_pointer]({{ site.url }}/images/git_diagrams/git_head_pointer.png)

`git branch experiment` command only creates a new pointer to the current head commit. In order to switch and start your development on the new experiment branch, you need to run `git checkout experiment` command. HEAD pointer now points to experiment branch.

{% highlight html %}
$ git checkout experiment
{% endhighlight %}

![git_co_experiment]({{ site.url }}/images/git_diagrams/git_co_experiment.png)

We'll go ahead and start experimenting our feature in the experiment.js file. After some testing, we confirm that our experiment feature succeded and we are ready to commit! We'll go ahead and commit the changes into the experiment branch. We'll see a new commit, C4.

{% highlight html %}
$ mvim experiment.js
$ git commit -m "create new button object" 
{% endhighlight %}

![git_commit_from_exp_branch]({{ site.url }}/images/git_diagrams/git_commit_from_exp_branch.png)

Since we have finish with our experiment, we may want to switch back to our master branch and continue our developement. We can do that using the checkout command like how we did earlier `git checkout master`. This command will move the HEAD pointer back to master and revert the files in our working directory to the snapshot of commit 3 (C3).

{% highlight html %}
$ git checkout master
$ mvim experiment.js
$ git commit -m "print msg to console" 
{% endhighlight %}

Let's make changes to the experiment.js file from our master branch and commit the changes. Doing this would cause the git project history to diverge. 

![git_commit_from_master]({{ site.url }}/images/git_diagrams/git_commit_from_master.png)

I have created a git project based on the illustration. Below is a screen shot from gitk, a commit viewer for git. In this git project history, we have a total of 5 commits and 2 branches(master and experiment). We'll talk about `rebase` and `merge` next to see how we can integrate the changes done on one branch to the other. 

![gitk_all]({{ site.url }}/images/git_diagrams/gitk_all.png)

# Git merge and git rebase
We have seen that `git branch` allow us to create new branches on git and start development from the newly created branch leaving our master branch independent of the new branch. This feature is very useful for developers to do experiment and allow every developer to work independently at their own branch. `git branch` causes the git project history to diverge so how can we integrate the changes? Git offers `git merge` command to merge the changes on the branch. Asides from `git merge`, `git rebase` also allow us to integrate the changes done on one branch to the other. Below is an example of `git merge` and `git rebase` ran with the HEAD pointer pointing at the master branch.

![git_merge_rebase]({{ site.url }}/images/git_diagrams/git_merge_rebase.png)

Another example I have below is running `git merge` and `git rebase` with the HEAD pointer pointing at the experiment branch.

![git_merge_rebase_experiment]({{ site.url }}/images/git_diagrams/git_merge_rebase_experiment.png)

The key takeaways from this is that `git merge` and `git rebase` will integrate the changes done on one branch to the other. However, how git does the integration in `git merge` and `git rebase` are different. Also, depending on the branch when you run the `git rebase` command, the result seen from the git commit view is different. Below are some recommended reference for the git commands discussed above:

* [git branch](http://git-scm.com/book/en/Git-Branching-What-a-Branch-Is) 
* [git rebase](http://git-scm.com/book/en/Git-Branching-Rebasing)
