# GIT INITIATE

$ git init

```

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~
$ mkdir myproject

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~
$ cd myproject

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/myproject
$ git init
Initialized empty Git repository in C:/Users/KLSDEVOPS/myproject/.git/

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/myproject (master)
$

```

# GIT CLONE
To clone an existing remote repository

$ git clone _REPO-URL_

```
KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~
$ git clone https://github.com/klsdevops/klsdevops.git
Cloning into 'klsdevops'...
remote: Enumerating objects: 147, done.
remote: Counting objects: 100% (147/147), done.
remote: Compressing objects: 100% (89/89), done.
remote: Total 147 (delta 52), reused 144 (delta 50), pack-reused 0
Receiving objects: 100% (147/147), 49.50 KiB | 1.41 MiB/s, done.
Resolving deltas: 100% (52/52), done.

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~
$
```

# GIT BRANCH

### LIST BRANCHES
$ git branch

### LIST ALL BRANCHES
$ git branch -a

### CREATE A NEW BRANCH

$ git branch _new-branch-name_ 

```
KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$ git branch
* main

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$ git branch -a
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$ git branch feature-branch

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$ git branch
  feature-branch
* main

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$

```
## SWITCH TO ANOTHER BRANCH

$ git checkout _branch-name_

```

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$ git checkout feature-branch
Switched to branch 'feature-branch'

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$

```

## ADD NEW FILES TO THE NEW BRANCH

```
KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$ ls -ltr
total 5
drwxr-xr-x 1 KLSDEVOPS 197121   0 Sep 29 08:22 Git/
drwxr-xr-x 1 KLSDEVOPS 197121   0 Sep 29 08:22 Jenkins/
-rw-r--r-- 1 KLSDEVOPS 197121 423 Sep 29 08:22 README.md

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$ echo "this is a test file" > test-file

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$ git status
On branch feature-branch
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test-file

nothing added to commit but untracked files present (use "git add" to track)

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$ git add test-file
warning: LF will be replaced by CRLF in test-file.
The file will have its original line endings in your working directory

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$ git status
On branch feature-branch
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   test-file


KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$ git commit -m "adding test file"
[feature-branch 5c5398f] adding test file
 1 file changed, 1 insertion(+)
 create mode 100644 test-file

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$ git status
On branch feature-branch
nothing to commit, working tree clean

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$ ls -ltr
total 6
drwxr-xr-x 1 KLSDEVOPS 197121   0 Sep 29 08:22 Git/
drwxr-xr-x 1 KLSDEVOPS 197121   0 Sep 29 08:22 Jenkins/
-rw-r--r-- 1 KLSDEVOPS 197121 423 Sep 29 08:22 README.md
-rw-r--r-- 1 KLSDEVOPS 197121  20 Sep 29 08:41 test-file

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$

```
## SET REMOTE AS UPSTREAM FOR A BRANCH & PUSH CHANGES TO REMOTE REPOSITORY

$ git push --set-upstream origin _branch-name_

```

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$ git push --set-upstream origin feature-branch
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 290 bytes | 290.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote:
remote: Create a pull request for 'feature-branch' on GitHub by visiting:
remote:      https://github.com/klsdevops/klsdevops/pull/new/feature-branch
remote:
To https://github.com/klsdevops/klsdevops.git
 * [new branch]      feature-branch -> feature-branch
Branch 'feature-branch' set up to track remote branch 'feature-branch' from 'origin'.

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$

```

## MERGE BRANCH
$ git merge _branch-name_

```

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (feature-branch)
$ git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$ git merge feature-branch
Updating 76697b9..5c5398f
Fast-forward
 test-file | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 test-file

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$

```

## DELETE A BRANCH
$ git branch -d _branch-name_

```

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$ git branch
  feature-branch
* main

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$ git branch -d feature-branch
Deleted branch feature-branch (was 5c5398f).

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$ git branch
* main

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/klsdevops (main)
$

```

## PRUNE REMOTE REPOSITORY BRANCHES
If the remote branches are already deleted & you still have your remote references in your local, you can prune it from local.

![image](https://user-images.githubusercontent.com/90503660/135725985-cf2d0a1e-95c5-4035-ba1a-b8b97d62e20b.png)

# GIT TAGS

**_List Tags:_**

```

$ git tag
v1.0
v2.0

```

**Search for tags that match a particular pattern:**

```

$ git tag -l "v1.8.5*"
v1.8.5
v1.8.5-rc0
v1.8.5-rc1
v1.8.5-rc2
v1.8.5-rc3
v1.8.5.1
v1.8.5.2
v1.8.5.3
v1.8.5.4
v1.8.5.5

```

**Create Annotated Tags:**

```

$ git tag -a v1.4 -m "my version 1.4"
$ git tag
v0.1
v1.3
v1.4

```

**To see the data of a tag:**

```

$ git show v1.4
tag v1.4
Tagger: Ben Straub <ben@straub.cc>
Date:   Sat May 3 20:19:12 2014 -0700

my version 1.4

commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Change version number

```

**Create Lightweight Tags:**

```

$ git tag v1.4-lw
$ git tag
v0.1
v1.3
v1.4
v1.4-lw
v1.5

```

**To tag a previous/old commit:**

```

$ git log --pretty=oneline
15027957951b64cf874c3557a0f3547bd83b3ff6 Merge branch 'experiment'
a6b4c97498bd301d84096da251c98a07c7723e65 Create write support
0d52aaab4479697da7686c15f77a3d64d9165190 One more thing
6d52a271eda8725415634dd79daabbc4d9b6008e Merge branch 'experiment'
0b7434d86859cc7b8c3d5e1dddfed66ff742fcbc Add commit function
4682c3261057305bdd616e23b64b0857d832627b Add todo file
166ae0c4d3f420721acbb115cc33848dfcc2121a Create write support
9fceb02d0ae598e95dc970b74767f19372d61af8 Update rakefile
964f16d36dfccde844893cac5b347e7b3d44abbc Commit the todo
8a5cbc430f1a9c3d00faaeffd07798508422908a Update readme

$ git tag -a v1.2 9fceb02

$ git tag
v0.1
v1.2
v1.3
v1.4
v1.4-lw
v1.5

$ git show v1.2
tag v1.2
Tagger: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Feb 9 15:32:16 2009 -0800

version 1.2
commit 9fceb02d0ae598e95dc970b74767f19372d61af8
Author: Magnus Chacon <mchacon@gee-mail.com>
Date:   Sun Apr 27 20:43:35 2008 -0700

    Update rakefile

```

**To transfer single tag to remote:**

```

$ git push origin v1.5
Counting objects: 14, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (12/12), done.
Writing objects: 100% (14/14), 2.05 KiB | 0 bytes/s, done.
Total 14 (delta 3), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.5 -> v1.5

```

**To transfer all tag to remote:**

```

$ git push origin --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 160 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.4 -> v1.4
 * [new tag]         v1.4-lw -> v1.4-lw

```

**Delete tags:**

```

$ git tag -d v1.4-lw
Deleted tag 'v1.4-lw' (was e7d5add)

```

**Delete remote tag:**

```

$ git push origin --delete <tagname>

```

**View version of files in a tag:**

```

$ git checkout v2.0.0
Note: switching to 'v2.0.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 99ada87... Merge pull request #89 from schacon/appendix-final

$ git checkout v2.0-beta-0.1
Previous HEAD position was 99ada87... Merge pull request #89 from schacon/appendix-final
HEAD is now at df3f601... Add atlas.json and cover image

```

In “detached HEAD” state, if you make changes and then create a commit, the tag will stay the same, but your new commit won’t belong to any branch and will be unreachable, except by the exact commit hash.

**To make changes from a tag & create new commits:**

Scenario: You want to fix a bug from an older version of release.
Create a new branch from the release tag & work on your bugfix & commit the changes.

```

$ git checkout -b version2 v2.0.0
Switched to a new branch 'version2'

```

# GIT BLAME

The git blame command is used to examine the contents of a file line by line and see when each line was last modified and who the author of the modifications was.

```

$ git blame README.md
82496ea3 (kevzettler     2018-02-28 13:37:02 -0800  1) # Git Blame example
82496ea3 (kevzettler     2018-02-28 13:37:02 -0800  2)
89feb84d (Albert So      2018-03-01 00:54:03 +0000  3) This repository is an example of a project with multiple contributors making commits.
82496ea3 (kevzettler     2018-02-28 13:37:02 -0800  4)
82496ea3 (kevzettler     2018-02-28 13:37:02 -0800  5) The repo use used elsewhere to demonstrate `git blame`
82496ea3 (kevzettler     2018-02-28 13:37:02 -0800  6)
89feb84d (Albert So      2018-03-01 00:54:03 +0000  7) Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod TEMPOR incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in 
voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum
89feb84d (Albert So      2018-03-01 00:54:03 +0000  8)
eb06faed (Juni Mukherjee 2018-03-01 19:53:23 +0000  9) Annotates each line in the given file with information from the revision which last modified the line. Optionally, start annotating from the given revision.
eb06faed (Juni Mukherjee 2018-03-01 19:53:23 +0000 10)
548dabed (Juni Mukherjee 2018-03-01 19:55:15 +0000 11) Creating a line to support documentation needs for git blame.
548dabed (Juni Mukherjee 2018-03-01 19:55:15 +0000 12)
548dabed (Juni Mukherjee 2018-03-01 19:55:15 +0000 13) Also, it is important to have a few of these commits to clearly reflect the who, the what and the when. This will help Kev get good screenshots when he runs the git blame on this README.
$

```

# Undoing Commits & Changes

**To review history of a GIT Repository:**

```

$ git log --oneline

```

**To visit a specific commit history & view files/changes:**

```

$ git checkout <commit-id>

eg;
$ git checkout 89feb84
Note: switching to '89feb84'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 89feb84 README.md edited online with Bitbucket

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example ((89feb84...))
$ ls -ltr
total 4
-rw-r--r-- 1 KLSDEVOPS 197121 775 Sep 26 13:44 README.md

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example ((89feb84...))
$ cat README.md 
# Git Blame example

This repository is an example of a project with multiple contributors making commits.

The repo use used elsewhere to demonstrate `git blame`

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod TEMPOR incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum

Annotates each line in the given file with information from the revision which last modified the line. Optionally, start annotating from the given revision.
KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example ((89feb84...))
$

```

**Undo commit with git checkout: (not an appropriate method)**

```

$ git checkout <commit-id>

then

$ git checkout -b <new-branch>

Now, this branch will not have any later commit history post the checkedout <commit-id>.
Unfortunately, if you need the previous branch, maybe it was your main branch, this undo strategy is not appropriate. 

```

**Undo a commit with GIT Revert:**

A revert is an operation that takes a specified commit and creates a new commit which inverses the specified commit. git revert can only be run at a commit level scope and has no file level functionality.

```


KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$ git log --oneline
6177785 (HEAD -> master, testrebasebr) another commit before rebase
a21d0bc some test file before rebase
eb758ef (origin/master, origin/HEAD) for testing rebase
69c2d83 (test-cherry) adding cherry3
dba2598 adding cherry2
ea9674c adding cherry1
487f630 rebase additions
2e7d73c fix for cherry
a5271b9 merge conflicts resolved
421900a added contents from master
00f6945 (branch_for_conflict) some contents added to README
f798562 Merging branch '3way-feature' to master
fdb6770 added new file from master
3835b19 (3way-feature) commiting on 3 way branch
d9a5ef6 (new-feature) added contents for merge
be32b99 Initial commit

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$ ls -ltr
total 9
-rw-r--r-- 1 KLSDEVOPS 197121   0 Feb 10 21:20 testfile
-rw-r--r-- 1 KLSDEVOPS 197121 137 Feb 10 21:51 README.md
-rw-r--r-- 1 KLSDEVOPS 197121  35 Feb 13 19:44 fix
-rw-r--r-- 1 KLSDEVOPS 197121   9 Feb 13 20:40 testrebase
-rw-r--r-- 1 KLSDEVOPS 197121  18 Feb 13 20:42 cherry1
-rw-r--r-- 1 KLSDEVOPS 197121  19 Feb 13 20:42 cherry2
-rw-r--r-- 1 KLSDEVOPS 197121  18 Feb 13 20:42 cherry3
-rw-r--r-- 1 KLSDEVOPS 197121  28 Feb 14 07:55 rebase
-rw-r--r-- 1 KLSDEVOPS 197121  23 Feb 14 07:57 sometest
-rw-r--r-- 1 KLSDEVOPS 197121  38 Feb 14 07:57 anothertest

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$ cat README.md
# branch-testing-repo
adding some content for 3 way merge
adding a line from 3way branch
adding some contents from the master branch

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$ vi README.md

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$ git add .

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$ git commit -m "needs to be removed"
[master a8bc814] needs to be removed
 1 file changed, 1 insertion(+)

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$ git log --oneline
a8bc814 (HEAD -> master) needs to be removed
6177785 (testrebasebr) another commit before rebase
a21d0bc some test file before rebase
eb758ef (origin/master, origin/HEAD) for testing rebase
69c2d83 (test-cherry) adding cherry3
dba2598 adding cherry2
ea9674c adding cherry1
487f630 rebase additions
2e7d73c fix for cherry
a5271b9 merge conflicts resolved
421900a added contents from master
00f6945 (branch_for_conflict) some contents added to README
f798562 Merging branch '3way-feature' to master
fdb6770 added new file from master
3835b19 (3way-feature) commiting on 3 way branch
d9a5ef6 (new-feature) added contents for merge
be32b99 Initial commit

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$ cat README.md
# branch-testing-repo
adding some content for 3 way merge
adding a line from 3way branch
adding some contents from the master branch
this needs to be removed

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$ git revert HEAD
[master 9b2b110] Revert "needs to be removed"
 1 file changed, 1 deletion(-)

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$ cat README.md
# branch-testing-repo
adding some content for 3 way merge
adding a line from 3way branch
adding some contents from the master branch

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$ git log --oneline
9b2b110 (HEAD -> master) Revert "needs to be removed"
a8bc814 needs to be removed
6177785 (testrebasebr) another commit before rebase
a21d0bc some test file before rebase
eb758ef (origin/master, origin/HEAD) for testing rebase
69c2d83 (test-cherry) adding cherry3
dba2598 adding cherry2
ea9674c adding cherry1
487f630 rebase additions
2e7d73c fix for cherry
a5271b9 merge conflicts resolved
421900a added contents from master
00f6945 (branch_for_conflict) some contents added to README
f798562 Merging branch '3way-feature' to master
fdb6770 added new file from master
3835b19 (3way-feature) commiting on 3 way branch
d9a5ef6 (new-feature) added contents for merge
be32b99 Initial commit

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 ~/Desktop/branch-testing-repo (master)
$


OR

$ git revert <commit-id>

```

Unlike our previous checkout strategy, we can continue using the same branch. This solution is a satisfactory undo. This is the ideal 'undo' method for working with public shared repositories. If you have requirements of keeping a curated and minimal Git history this strategy may not be satisfactory.

**Undo a commit with GIT Reset:**

A reset is an operation that takes a specified commit and resets the "three trees" to match the state of the repository at that specified commit. A reset can be invoked in three different modes which correspond to the three trees.

A simple git reset will not reset the contents of the file, it will just reset the commit history & we will have to add/remove the content of file manually with further commands(git restore/git add) 

But a "git reset --hard" will reset the file content along with the commit history.

If we invoke "git reset --hard 990c2b6" the commit history is reset to that specified commit. 

```

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git log --oneline
439aac1 (HEAD -> master) Revert "Another commit to help git blame track the who, the what, and the when"
548dabe (origin/master, origin/HEAD) Another commit to help git blame track the who, the what, and the when
eb06fae Creating the third commit, along with Kev and Albert, so that Kev can get git blame docs.
990c2b6 Merged in albert-so/git-blame-example/albert-so/readmemd-edited-online-with-bitbucket-1519865641474 (pull request #2)
89feb84 README.md edited online with Bitbucket
82496ea add some filler content to the README
fefb662 initial commit add empty readme

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git reset --hard 990c2b6
HEAD is now at 990c2b6 Merged in albert-so/git-blame-example/albert-so/readmemd-edited-online-with-bitbucket-1519865641474 (pull request #2)

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git log --oneline
990c2b6 (HEAD -> master) Merged in albert-so/git-blame-example/albert-so/readmemd-edited-online-with-bitbucket-1519865641474 (pull request #2)
89feb84 README.md edited online with Bitbucket
82496ea add some filler content to the README
fefb662 initial commit add empty readme

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$

```

This method of undoing changes has the cleanest effect on history. Doing a reset is great for local changes however it adds complications when working with a shared remote repository. 

If we have a shared remote repository that has the eb06fae commit pushed to it, and we try to git push a branch where we have reset the history, Git will catch this and throw an error. Git will assume that the branch being pushed is not up to date because of it's missing commits. In these scenarios, git revert should be the preferred undo method.

**NOTE:** Checkout and reset are generally used for making local or private 'undos'. They modify the history of a repository that can cause conflicts when pushing to remote shared repositories. Revert is considered a safe operation for 'public undos' as it creates new history which can be shared remotely and doesn't overwrite history remote team members may be dependent on.

**Undoing the last commit:**

In some cases though, you might not need to remove or reset the last commit. Maybe it was just made prematurely. In this case you can amend the most recent commit. Once you have made more changes in the working directory and staged them for commit by using "git add", you can execute "git commit --amend". 

**Undoing uncommitted changes:**

```

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git status
On branch master
Your branch is behind 'origin/master' by 2 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git log --oneline
990c2b6 (HEAD -> master) Merged in albert-so/git-blame-example/albert-so/readmemd-edited-online-with-bitbucket-1519865641474 (pull request #2)
89feb84 README.md edited online with Bitbucket
82496ea add some filler content to the README
fefb662 initial commit add empty readme

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ ls -ltr
total 4
-rw-r--r-- 1 KLSDEVOPS 197121 775 Sep 26 14:23 README.md

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ vi README.md

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git status
On branch master
Your branch is behind 'origin/master' by 2 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ cat  README.md 
# Git Blame example
this is an unwanted line

This repository is an example of a project with multiple contributors making commits.

The repo use used elsewhere to demonstrate `git blame`

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod TEMPOR incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum

Annotates each line in the given file with information from the revision which last modified the line. Optionally, start annotating from the given revision.

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git restore README.md

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ cat README.md 
# Git Blame example

This repository is an example of a project with multiple contributors making commits.

The repo use used elsewhere to demonstrate `git blame`

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod TEMPOR incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum

Annotates each line in the given file with information from the revision which last modified the line. Optionally, start annotating from the given revision.
KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git status
On branch master
Your branch is behind 'origin/master' by 2 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$

```

**GIT rm command:**

A common question when getting started with Git is "How do I tell Git not to track a file (or files) any more?" The git rm command is used to remove files from a Git repository. It can be thought of as the inverse of the git add command.

The primary function of git rm is to remove tracked files from the Git index. Additionally, git rm can be used to remove files from both the staging index and the working directory. 


# GIT STASH

The git stash command takes your uncommitted changes (both staged and unstaged), saves them away for later use, and then reverts them from your working copy. 

```

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git status
On branch rebase-branch
nothing to commit, working tree clean

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ vi README.md

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git status
On branch rebase-branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git add .

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git status
On branch rebase-branch
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md


KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$

#DURING THIS WORK IF YOU WANT TO WORK ON ANOTHER FEATURE, YOU CAN PUT THIS ON TO STASH

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git stash
Saved working directory and index state WIP on rebase-branch: 959d108 stasj

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git status
On branch rebase-branch
nothing to commit, working tree clean

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$

#NOW CHECKOUT TO ANOTHER BRANCH AND PERFORM YOUR OTHER WORK

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git checkout master 
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ vi test

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ cat test 
this is a new file

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test

nothing added to commit but untracked files present (use "git add" to track)

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git add .
warning: LF will be replaced by CRLF in test.
The file will have its original line endings in your working directory

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   test


KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git commit -m "added new file"
[master 33e513e] added new file
 1 file changed, 1 insertion(+)
 create mode 100644 test

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 4 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$

#ONCE THE WORK IS COMMITTED, CHECKOUT BACK TO THE PREVIOUS BRANCH & POP THE STASH OUT

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (master)
$ git checkout rebase-branch 
Switched to branch 'rebase-branch'

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git status
On branch rebase-branch
nothing to commit, working tree clean

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$

#TO LIST THE STASHES;

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git stash list
stash@{0}: WIP on rebase-branch: 959d108 stasj

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$

#TO SHOW THE FILES IN THE MOST RECENT STASHES;

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git stash show
 README.md | 1 +
 1 file changed, 1 insertion(+)

#SHOW THE CHANGES OF MOST RECENT STASHES;

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git stash show -p stash@{0}
diff --git a/README.md b/README.md
index 0ce4e4c..25906d9 100644
--- a/README.md
+++ b/README.md
@@ -1,4 +1,5 @@
 # Git Blame example
+testing stash
 This repository is an example of a project with multiple contributors making commits.

 The repo use used elsewhere to demonstrate `git blame`

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ 

#TO POP OUT THE PREVIOUS CHANGES FROM STASH 

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git stash pop
On branch rebase-branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (df3b99446de5ab67570a357b2815cbd8d6b584a9)

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$

#COMMIT THE CHANGES

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git status
On branch rebase-branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git add .

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git status
On branch rebase-branch
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md


KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git commit -m "commit after stash"
[rebase-branch 012b919] commit after stash
 1 file changed, 1 insertion(+)

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$ git status
On branch rebase-branch
nothing to commit, working tree clean

KLSDEVOPS@LAPTOP-SME4GNLK MINGW64 /d/DevOps/KLSDevOps Trainings/Sept 2021/GIT/git-blame-example (rebase-branch)
$

```
# TO SEE THE GRAPHICAL REPRESENTATION OF LOGS

```
git log --graph
```

![image](https://user-images.githubusercontent.com/90503660/152688819-2d5dfad2-5e3c-444c-b4af-8e1a536d50c5.png)


### Graph all git branches decorated with colour & oneline

```
git log --all --decorate --oneline --graph
```
![image](https://user-images.githubusercontent.com/90503660/152689112-97b6ebe2-87dd-4244-8d8d-7a807de5ded2.png)

