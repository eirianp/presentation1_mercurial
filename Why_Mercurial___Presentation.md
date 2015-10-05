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
	* If she wants to switch to an older revision, she must download it from the central repository
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

## Dive into distributed version control with Mercurial
* Mercurial has a similar interface to Git:

> eiriano> hg help <br>
> Mercurial Distributed SCM <br>
>  <br>
> list of commands: <br>
>  <br>
>  add           add the specified files on the next commit <br>
>  addremove     add all new files, delete all missing files <br>
>  annotate      show changeset information by line for each file <br>
>  archive       create an unversioned archive of a repository revision <br>
>  backout       reverse effect of earlier changeset <br>
>  bisect        subdivision search of changesets <br>
>  bookmarks     create a new bookmark or list existing bookmarks <br>
>  branch        set or show the current branch name <br>
>  branches      list repository named branches <br>
>  bundle        create a changegroup file <br>
>  cat           output the current or given revision of files <br>
>  clone         make a copy of an existing repository <br>
>  commit        commit the specified files or all outstanding changes <br>
>  config        show combined config settings from all hgrc files <br>
>  copy          mark files as copied for the next commit <br>
>  diff          diff repository (or selected files) <br>
>  export        dump the header and diffs for one or more changesets <br>
>  files         list tracked files <br>
>  forget        forget the specified files on the next commit <br>
>  graft         copy changes from other branches onto the current branch <br>
>  grep          search for a pattern in specified files and revisions <br>
>  heads         show branch heads <br>
>  help          show help for a given topic or a help overview <br>
>  identify      identify the working directory or specified revision <br>
>  import        import an ordered set of patches <br>
>  incoming      show new changesets found in source <br>
>  init          create a new repository in the given directory <br>
>  log           show revision history of entire repository or files <br>
>  manifest      output the current or given revision of the project manifest <br>
>  merge         merge another revision into working directory <br>
>  outgoing      show changesets not found in the destination <br>
>  paths         show aliases for remote repositories <br>
>  phase         set or show the current phase name <br>
>  pull          pull changes from the specified source <br>
>  push          push changes to the specified destination <br>
>  recover       roll back an interrupted transaction <br>
>  remove        remove the specified files on the next commit <br>
>  rename        rename files; equivalent of copy + remove <br>
>  resolve       redo merges or set/view the merge status of files <br>
>  revert        restore files to their checkout state <br>
>  root          print the root (top) of the current working directory <br>
>  serve         start stand-alone webserver <br>
>  status        show changed files in the working directory <br>
>  summary       summarize working directory state <br>
>  tag           add one or more tags for the current or given revision <br>
>  tags          list repository tags <br>
>  unbundle      apply one or more changegroup files <br>
>  update        update working directory (or switch revisions) <br>
>  verify        verify the integrity of the repository <br>
>  version       output version and copyright information <br>
>  <br>
> enabled extensions: <br>
> <br> 
>  shelve        save and restore changes to the working directory <br>
>  <br>
> additional help topics: <br>
>  <br>
>  config        Configuration Files <br>
>  dates         Date Formats <br>
>  diffs         Diff Formats <br>
>  environment   Environment Variables <br>
>  extensions    Using Additional Features <br>
>  filesets      Specifying File Sets <br>
>  glossary      Glossary <br>
>  hgignore      Syntax for Mercurial Ignore Files <br>
>  hgweb         Configuring hgweb <br>
>  merge-tools   Merge Tools <br>
>  multirevs     Specifying Multiple Revisions <br>
>  patterns      File Name Patterns <br>
>  phases        Working with Phases <br>
>  revisions     Specifying Single Revisions <br>
>  revsets       Specifying Revision Sets <br>
>  scripting     Using Mercurial from scripts and automation <br>
>  subrepos      Subrepositories <br>
>  templating    Template Usage <br>
>  urls          URL Paths <br>
>  <br>
> (use "hg help -v" to show built-in aliases and global options) <br>

<br><br><br><br><br>

## Dive into distributed version control with Mercurial -- The Basics
* Mercurial has a similar interface to Git.
* In fact, Git and Mercurial resemble each other because they *borrow features* [from each other.](http://stackoverflow.com/questions/1598759/git-and-mercurial-compare-and-contrast)
* Let's see some examples:
	* type `hg init` to create a new repository. A .hg directory will be created in the current working directory.
	* Next, try to add some files to the repository with `hg add`.
	* What did you notice?  `hg add` will add everything in the current directory to the repository. Does your directory have hidden files? If you are also in a Git repository, for example, every file will be recursivly added, even if it's in a hidden file or directory (for example .git/).
	* If that's not what you wanted, simple do an `hg revert` or `hg revert --all` to revert everything in the current directory to what it was at the last commit.
	* Ok, let's try that again. Do an `hg add foo.txt` to add `foo.txt` to the repository only.
	* Do an `hg status` to see which files have changed. This is roughly equivalent to `svn status -u`.
		* Mercurial gives character codes similar to SVN:
			* ! missing
			* ? unknown
			* M modified
			* R removed
			* A added
	* Next, try an `hg commit` to commit changes to your local repository. Unlike Git, there is no need to `hg add foo.txt` again.
	* A log of revision changes are viewable with `hg log`. Like Git, these are also viewable as a graph with `hg log --graph`. 
		* You might notice a hash value by the revision number. Both Git and Mercurial use a SHA1 hash to create hash values for some changeset.
	* Like SVN, you can view diffs against the head revision with `hg diff <filename>`. It is also possible to compare diffs from a file from any revision using `hg diff <filename> -r x:y` where x and y are revisions of interest.
	* You may also view diffs with `hg cat <filename> -r x:y`. Or, view any revision of a file without moving your repository to a different branch or changeset: `hg cat <filename> -r x`. Again, x is a revision of interest.
	* `hg update` may be used to go to any specified revision. This is similar to `git checkout`.
	* `hg update` without any arguments will simply take you to the newest revision.
<br><br><br><br><br>

## Dive into distributed version control with Mercurial -- The Basics
* `hg push` is about the same as `git push`. 
* `hg pull` is about the same as `git pull`. 
	* it's worth noting that `push` and `pull` operations do not automatically update the working copy to the head revision. 
	* you must perform an `hg up` to get to `tip` or the top of the change set.
* `hg incoming` and `hg outgoing` push/pull to the central repository, if one exists.
* Mercurial can also create a webserver with the `hg serve` command. Take a look:
![alt text](http://www.torsten-horn.de/img/mercurial-hg-serve.png "hg serve")
* Mercurial tells you where to navigate to in a web browser:
	* `listening at http://terminus.local:8000/ (bound to *:8000)`
	* this is roughly equivalent to `git instaweb`.
	* Personally, I find `hg serve` much more useful than `hg cat`'ing through different revisions. As a software developer, a web interface is useful to me when I want to see when a bug was introduced or fixed.
<br><br><br><br><br>

## Dive into distributed version control with Mercurial -- Reverting
* As we saw earlier, it's possible to discard changes and return to the last revision using `hg revert` or `hg revert --all`. This is equivalent to deleting any changed files and doing an `svn update`.
* That's great, but eventually I'm going to commit to a branch that management has under *CRB control* (Change Review Board -- maintenance only branches that require approval for checkins). 
* To get Larry the Product Owner off my case, I can quickly undo the last commit with an `hg rollback`. 3 hours and 46 Googles later, I can figure out how to do this in SVN. By then, Larry would have noticed and I will have had to write apology cards to 4 different managers and India's CRB board.
* That's great too, but what if Earl got his CRB approved change into the branch moments after my bad commit? I can simply do an `hg backout -r x --merge` to remove my revision x from the branch. Note that this command may cause merge conflicts.
<br><br><br><br><br>

## Dive into distributed version control with Mercurial -- Merging
* Merging happens all the time. If Shannon and I are both working on foo.txt and she commits a change I need to keep working, I'll have to perform an `hg pull` to get her change. Most of the time, Mercurial will merge automatically.
* If Shannon and I were both working on the same part of the file, there will be a merge conflict that must be resolved manually. 
* It's also possible that there will be two "heads," for instance, Shannon and I both made changes on the most recent changeset.
* After merging, you should probably do a commit. Mercurial won't automatically commit after a merge.
* It's also worth noting that [Git supports an unlimited number of parents.](https://code.google.com/p/support/wiki/DVCSAnalysis). Mercurial supports 2 only. This means that you'll have to perform "N-1 two-way merges" in mercurial.
<br><br><br><br><br>

## Dive into distributed version control with Mercurial -- Change Sets
* As we saw earlier, the hash values seen in the output from `hg log` uniquely identifies a revision.
* Mercurial also gives revision numbers, but these aren't unique. My revision 13 is probably different than Shannon's revision 13. 
* A "nice-to-have" feature that Mercurial offers is the ability to give a change set a unique name called a "tag."
* Use the command `hg tag <tagname>` to create a tag.
* Let's look at an example:

> eiriano> hg tag my-great-tag <br>
> eiriano> hg commit -m "adding tag" <br>
> eiriano> hg log <br>
> changeset:   3:a6848afc4a3b <br>
> tag:         tip <br>
> user:        eirian <br>
> date:        Sat Oct 03 20:09:50 2015 -0600 <br>
> summary:     adding tag <br>
> <br>
> changeset:   2:7b16732fea62 <br>
> user:        eirian <br>
> date:        Sat Oct 03 20:09:43 2015 -0600 <br>
> summary:     Added tag my-great-tag for changeset 8bc04e68e855 <br>
>  <br>
> changeset:   1:8bc04e68e855 <br>
> tag:         my-great-tag <br>
> user:        eirian <br>
> date:        Tue Sep 29 00:17:04 2015 -0600 <br>
> summary:     second commit, typing "hg commit" will commit all changed files. That's pretty convenient! <br>
>  <br>
> changeset:   0:8a935b4f88b5 <br>
> user:        eirian <br>
> date:        Tue Sep 29 00:14:58 2015 -0600 <br>
> summary:     adding notes.txt to first commit <br>

* Now this tag name can be used to jump to that changeset:

> hg up -r my-great-tag <br>

* you can do an hg up -r <tag> to go to a particular changeset:
	* `hg up -r my-great-tag`
* suppose my-great-tag was some version that gets shipped to a customer, and a bug has to get changed. You can hg up to it, make a change, and ship. That doesn't seem too much different than going to a branch on svn for the same reason.
* if you want this new change in head, you have to do an hg merge. Mercurial has a bug where the .hgtags file has a merge conflict (if some revisions have tags). Just make sure to leave every line in the file.
* alternatively, just clone one branch to another
	* `hg clone -r <foo> my-great-tag some-other-tag`
<br><br><br><br><br>


## But Git has X feature!
* Mercurial and Git have fairly similar features
* Can't find feature X in Mercurial? Try looking for an extension.
* Consider Git's stash feature. This allows Git users to set aside changes they're not actively working on.
* For example, often times I like to fix compiler warnings. Since everyone says they're so busy all the time, it's hard to get these changes reviewed and accepted. I also don't want to accidentally `push` them to the central repository.
* So does Mercurial support this feature? Yes, through the *shelve extension*.
* To enable it, add `shelve=` under the `[extensions]` field in your .hgrc file.
	* `vim ~/.hgrc`

> \# example user config (see "hg help config" for more info) <br>
> [ui] <br>
> \# name and email, e.g.<br>
> \# username = Jane Doe <jdoe@example.com><br>
> username = eirian<br>
> <br>
> [extensions]<br>
> shelve=<br>
> \# uncomment these lines to enable some popular extensions<br>
> \# (see "hg help extensions" for more info)<br>
> \#<br>
> \# pager =<br>
> \# progress =<br>
> color=<br>

* You might also notice the `color=` line in my .hgrc file. As a second example, Mercurial does not have colorful output by default like Git does. This can also be enabled via the color extension. 
* Extensions may not be ideal because they must be configured and may have to be downloaded. 
<br><br><br><br><br>

## Git and Mercurial are pretty similar
* Both are distributed version control systems with a very similar feature set.
* One isn't necessarily "better" than the other. 
* What are the main differences?
	* You can't prune (discard) branches in Mercurial
	* Several authors suggest that Mercurial is easier to learn. I don't see much of a difference in learning curve.
	* Git has a larger community. Git has GitHub behind it and Mercurial his BitBucket. They're fairly similar.
	* Mercurial has better support for Windows developers. TortoiseHg is pretty similar to TortoiseSVN. The official Windows support for Git is through cygwin, which isn't that awesome.
	* The archetecture is fairly different. Git is more of an aggregate of C programs. Mercurial is more monolithic and implemented mostly in Python with some small amount of C. Mercurial supports third party extensions in the form of Python modules.
* The differences I noticed as a beginner were minimal. As mentioned earlier, Mercurial doesn't have colorful output enabled as a default. Mercurial also seems to be more verbose. 
* I created a Git and Mercurial repository in the same repository. Let's check out the differences:

#### Git:
> eiriano> git status <br>
> On branch master <br>
> Your branch is up-to-date with 'origin/master'. <br>
> Changes not staged for commit: <br>
>   (use "git add <file>..." to update what will be committed) <br>
>   (use "git checkout -- <file>..." to discard changes in working directory) <br>
>  <br>
> 	modified:   Why_Mercurial___Presentation.md <br>
>  <br>
> Untracked files: <br>
> 	  (use "git add <file>..." to include in what will be committed) <br>
> 			.hg/ <br>
> 			.hgtags <br>
> no changes added to commit (use "git add" and/or "git commit -a") <br>

#### Mercurial:
> eiriano> hg status
> ? .git/COMMIT_EDITMSG <br>
> ? .git/HEAD <br>
> ? .git/config <br>
> ? .git/description <br>
> ? .git/gitweb/gitweb_config.perl <br>
> ? .git/gitweb/lighttpd.conf <br>
> ? .git/gitweb/lighttpd/error.log <br>
> ? .git/hooks/applypatch-msg.sample <br>
> ? .git/hooks/commit-msg.sample <br>
> ? .git/hooks/post-update.sample <br>
> ? .git/hooks/pre-applypatch.sample <br>
> ? .git/hooks/pre-commit.sample <br>
> ? .git/hooks/pre-push.sample <br>
> ? .git/hooks/pre-rebase.sample <br>
> ? .git/hooks/prepare-commit-msg.sample <br>
> ? .git/hooks/update.sample <br>
> ? .git/index <br>
> ? .git/info/exclude <br>
> ? .git/logs/HEAD <br>
> ? .git/logs/refs/heads/master <br>
> ? .git/logs/refs/remotes/origin/master <br>
> ? .git/objects/00/8b8bff6d4b3d989fd68b3aab4330b6a304c117 <br>
> ? .git/objects/05/5c45b500c973ad1539bb3a9503d5bad47ff515 <br>
> ? .git/objects/08/f3575ce48ca655f01ea86dc32355c89cee810a <br>
> ? .git/objects/09/046d8644606d1c703372f019686a5813a1890f <br>
> ? .git/objects/0d/5fe10487748f9467e1ad948d40e25a2c32cc54 <br>
> ? .git/objects/0d/aa4a5a0a557d0134d97ad2132486457dd0ae14 <br>
> ? .git/objects/0e/8255a58aa75075532be4d8208c7d7a867f81fb <br>
> ? .git/objects/10/8bbb146ab7f0755d6e6fafca1611194653f957 <br>
> ? .git/objects/11/7d27938216d5b9e671c939cc18bfce308c2e75 <br>
> ? .git/objects/12/542ce8c53b8a4c306945623fc29833171d0b0f <br>
> ? .git/objects/16/031c9c380a8246630bbe31c6e3b2a1c9e17432 <br>
> ? .git/objects/1c/1cd735ed74b6bc41dbb84e21b90f9f4b07eecc <br>
> ? .git/objects/1c/6b7bafee6cecf3572cf8a3514cd7f59017eaca <br>
> ? .git/objects/1d/f11e569ebf2542a50df8a86b8159a4d2434f0e <br>
> ? .git/objects/1f/7b6fb2516a67ccfff52a08c98814ec19ccc550 <br>
> ? .git/objects/25/7cc5642cb1a054f08cc83f2d943e56fd3ebe99 <br>
> ? .git/objects/26/ac29f75afc0460e6b8c37e9149798935c8ee15 <br>
> ? .git/objects/26/dd5629c7cc835381628448d84fa10a8e0a1be8 <br>
> ? .git/objects/27/2df6243b40433d120f496718aca4f8d9270943 <br>
> ? .git/objects/29/12b4ca523cd5d9c21778f62a2134cf007beefd <br>
> ? .git/objects/2b/4600909f2703ba3404d2ceffa2307bd656b784 <br>
> ? .git/objects/2d/2d2b44dfb233fa46d260c8a4ecca24a776e931 <br>

* This continues for a long while. I truncated the output.
<br><br><br><br><br>

## Summary
* In a distributed version control system, every user has a complete and local repository.
* Both Git and Mercurial are distributed version control systems.
* "Traditional" version control systems use a central repository. This is possible but not required for Bit and Mercurial.
* Branching and merging are every day activities in Mercurial and are orders of magnitude easier to perform than in traditional version control systems. (It's possible that's an exaggeration.)
* Git and Mercurial are fairly similar in terms of features and interface, but Git is somewhat more popular.
* Distributed version control systems enhance communication and collaboration in a software engineering environment.
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
13. http://biz30.timedoctor.com/git-mecurial-and-cvs-comparison-of-svn-software/
