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
* What is a branch?
<br><br><br><br><br>

## Traditional version control -- advantages
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
* content from hginit goes here
<br><br><br><br><br>

## Why use version control?
* cohesiveness
* communication
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

