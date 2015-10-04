# Distributed Version Control with Mercurial
![alt text](https://www.selenic.com/hg-logo/logo-droplets-75.png "Mercurial logo from www.selenic.com")
### _Eirian O Perkins_
#
<br><br><br><br><br>

## Topics
* What problem does version control solve?
* Traditional Version Control
* Dive into distributed version control with Mercurial
* Summary
<br><br><br><br><br>


## What problem does version control solve?
* Version control keeps a history of changes
* This is useful for *individual contributors*
	* versions of a resume
* Version control allows you to _roll back_ changes
	* try out new code changes
	* Without a history of changes, how do I keep track of last stable version?
	* What if my changes broke code and I don't know how to fix it?
* What does life look like without version control?
	* Keep track of versions with timestamps
	* Or, a directory full of files with some numbering scheme
	* Without a log of commit messages, it's easy to forget the motivation behind changes
	* What if 2 different versions of the file  both have changes I want? Merging without a version control system would be painful
<br><br><br><br><br>

## What problem does version control solve?
* Let's consider a *team* instead of an individual contributor.
* Version control allows teams to
	* work together from different geographical locations
		* simply commit (or push) your changes to allow team members to benefit from your work
	* review the history of code changes. Suppose Bob was WFR'd (work force reduction) and I wanted to see what he was thinking when he made change X. I can look through the revision history to see commit messages and any comments he may have added.
	* submit changes to another person's code. Dan forgot to add a default case to his switch statement and all hell breaks loose. Shannon can go in and add this, making the world right again.
	* ___maintain multiple versions of a product___
		* Your organization may want to deploy different versions of the code base to customers
		* Different features may have different price points
		* Newer code may not work on older hardware
		* Your organization may not have the resources to test every version of the code on every supported platform
		* Do you really want to keep updating gen 6 software when you're trying to sell gen 10 solutions? You may want to mark the gen 6 codebase as *maintenance only*
<br><br><br><br><br>

## Traditional version control
* Subversion (SVN) is a classic example of traditional version control.
* In the traditional model, there is a central repository
* The central repository contains all the revision history
* Local copies, for instance in Shannon's directory, have one version of the code base only.
	* If she wants to switch to an older revision, she must make a request to the central repository
<br><br><br><br><br>

## Traditional version control -- basic concepts
* Let's review concepts through *use cases*
	* checking out
		* Earl the new hire joins our team. The first thing we'd like him to do is *check out* the latest code from *trunk*, the active development branch
		* Shannon would like to *check out* Dan's private branch so that she can pair program with him and make changes without affecting *trunk*.
		* Cory *checks out* a legacy branch for gen 6 in order to investigate and resolve a defect customers are still complaining about.
	* committing
		* Once Shannon has added feature or resolved a defect, she needs to *commit* her change so that it is visable to her teammates. This allows the build team to create a *nightly build* with all the new changes from the previous day.
	* branching
		* A *branch* is a copy of the code from some *revision*, or a point in time
		* After so many *iterations* in the software development lifecycle, Larry the product owner will create a gen 9 branch, which will then become maintenance only, and all the developers will happily continue developing on trunk, which will be for gen 10 until the next product branch.
		* Shannon may create her own branch for development purposes and share it with her teammates. Once she's satisfied with her changes, she can *merge* them with trunk
	* merging
		* Merging applies changes from one code source to another.
		* One branch may be merged to another, for example
<br><br><br><br><br>


## Traditional version control -- advantages
* The administrator has control over "who can do what"
	* The administrator determines where and when to *branch*
	* The administrator determines who can add changes
		* Shannon shouldn't be making un-approved and un-tested changes to a maintenance only branch
* Plus, all the motivations for revision control we saw earlier
<br><br><br><br><br>

## Traditional version control -- short comings
* single point of failure
	* what happens when the central repository is unavailable?
	* what if your repository is on a single disk (no redundancy) and the disk fails?
		* this happened regularly at the first company I worked at
* _Committing_ to the central repository inflicts your changes on all teammates
	* What if Dan and Shannon wanted to pair program before submitting changes
<br><br><br><br><br>

## Traditional version control -- Pitfalls from a consultant's perspective
* The folks at [Kiln](http://hginit.com/) see the same story over and over
	* Teams want to create a branch so that the development branch is separate from the shipping branch (what gets delivered to customers).
	* This is fine until the team tries to *merge*. Merging is a nightmare
	* It takes "six programmers around a single computer working for two weeks trying to manually reapply every single bug fix from the stable build back into the development build."
	* Alternatively, each new feature "is in a big #ifdef block."
* I see the same problem at my job with SVN
	* a big committee decides who can check in what to which branch
	* each developer needs approval
	* automatic merging is forbidden -- every merge must be done by hand
<br><br><br><br><br>

## How is distributed version control different?
* With a *distributed version control system*, each developer [has the entire repository.](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)
	* Yes, the entire repository. A developer has all the branches, revisions, logs, etc. [All "diffs, commits, and reverts are done locally."](http://betterexplained.com/articles/intro-to-distributed-version-control-illustrated/)
	* Merging is an every-day activity and is easy *by nature*
		* distributed version control systems like Git and Mercurial track changes at the directory level instead of single files
* This enables workflows that are difficult or impossible with traditional version control systems
	* Shannon and Dan can share their local changes with each other without inflicting them on the entire team
	* It's possible to work *offline* (committing, branching, merging, etc.)
	* There's no more "giant checkins" because each developer will have their incremental history
* it is still possible to have a central repository 
* This shift in functionality improves _communication_ between teammates
	* Communication is the key to engineering!

* The figures below from [Kiln](http://hginit.com) illustrate the difference:
### Traditional version control
![alt text](http://hginit.com/i/00-svn.png "traditional version control")
### Distributed version control
![alt text](http://hginit.com/i/00-hg.png "distributed version control")
<br><br><br><br><br>


## References
1. http://hginit.com/
2. http://stackoverflow.com/questions/1408450/why-should-i-use-version-control
3. http://soundsoftware.ac.uk/why-version-control
4. https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control
5. http://margotskapacs.com/2012/10/shelving-uncommitted-changes-in-mercurial/
6. http://codeyarns.com/2014/04/11/how-to-use-shelve-extension-of-mercurial/
7. http://tortoisehg.bitbucket.org/manual/0.9/shelve.html
8. http://stackoverflow.com/questions/11520047/how-do-i-put-a-bunch-of-uncommitted-changes-aside-while-working-on-something-els
9. http://ndpsoftware.com/git-cheatsheet.html
10. https://code.google.com/p/support/wiki/DVCSAnalysis
11. http://stevelosh.com/blog/2010/01/the-real-difference-between-mercurial-and-git/
12. http://stackoverflow.com/questions/1598759/git-and-mercurial-compare-and-contrast

