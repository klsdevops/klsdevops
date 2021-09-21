# **Git Merge:**

* The git merge command lets you take the independent lines of development created by git branch and integrate them into a single branch.
* Git merge will combine multiple sequences of commits into one unified history.
* In the most frequent use cases, git merge is used to combine two branches.
* During merge conflicts, Git will need user intervention to continue. 

**Preparing to merge:** Before performing a merge there are a couple of preparation steps to take to ensure the merge goes smoothly.

**Confirm the receiving branch:** Execute git status to ensure that HEAD is pointing to the correct merge-receiving branch. 

  ```$ git checkout main```
  
**Fetch latest remote commits:** Make sure the receiving branch and the merging branch are up-to-date with the latest remote changes.

```$ git pull_ OR _git fetch```
  
**Merging:** A merge can be initiated by executing git merge where  is the name of the branch that will be merged into the receiving branch.

```$ git merge feature_branch```

## Fast Forward Merge
* A fast-forward merge can occur when there is a linear path from the current branch tip to the target branch.
* Instead of “actually” merging the branches, all Git has to do to integrate the histories is move (i.e., “fast forward”) the current branch tip up to the target branch tip.

<p align="center">
  <img src="https://user-images.githubusercontent.com/90503660/133953717-10804480-1faf-4534-9fd0-41157709cb96.png"> 
</p>
  
```
### CREATE A NEW FILE AND COMMIT TO THE REPO

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ touch test

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test

nothing added to commit but untracked files present (use "git add" to track)

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git add .

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   test


klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git commit -m "first commit"
[master (root-commit) cc9cab9] first commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git status
On branch master
nothing to commit, working tree clean

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git branch
* master

### CREATE A NEW FEATURE BRANCH "new-feature" 

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git checkout -b new-feature master
Switched to a new branch 'new-feature'

### UPDATE A FILE IN THE NEW FEATURE BRANCH AND COMMIT

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ vi test

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git add .
warning: LF will be replaced by CRLF in test.
The file will have its original line endings in your working directory

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git commit -m "second commit"
[new-feature afaf55f] second commit
 1 file changed, 1 insertion(+)

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git branch
  master
* new-feature

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git status
On branch new-feature
nothing to commit, working tree clean

### CHECK THE COMMIT HISTORY. YOU COULD SEE A NEW COMMIT HASH HAS BEEN CREATED AND THE HEAD OF FEATURE BRANCH IS POINTING TO IT

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git log --oneline
afaf55f (HEAD -> new-feature) second commit
cc9cab9 (master) first commit

### CHECKOUT TO "master" BRANCH AND CHECK THE COMMIT HISTORY. YOU COULD SEE ONLY ONE COMMIT & HEAD OF MASTER IS POINTING TO IT.

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git checkout master
Switched to branch 'master'

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git log --oneline
cc9cab9 (HEAD -> master) first commit

### MERGE THE FEATURE BRANCH TO MASTER BRANCH.

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git merge new-feature
Updating cc9cab9..afaf55f
Fast-forward
 test | 1 +
 1 file changed, 1 insertion(+)

### CHECK THE COMMIT HISTORY

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git log --oneline
afaf55f (HEAD -> master, new-feature) second commit
cc9cab9 first commit

### YOU COULD SEE THE HEAD HAS POINTED TO THE SAME COMMIT "afaf55f" AND BOTH MASTER AND FEATURE BRANCHES ARE POINTING TO THE SAME COMMIT.
### IN EFFECT, IT'S JUST AS FAST FORWARDING (MOVING) THE HEAD TO THE LATEST COMMIT OF THE TARGET BRANCH.

### NOW, DELETE THE FEATURE BRANCH AS IT IS ALREADY MERGED TO THE MASTER.

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git branch -d new-feature
Deleted branch new-feature (was afaf55f).

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git status
On branch master
nothing to commit, working tree clean

### CHECK THE COMMIT TO SEE THE HEAD OF MASTER IS POINTING TO THE LATEST COMMIT

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git log --oneline
afaf55f (HEAD -> master) second commit
cc9cab9 first commit

```

## 3-Way Merge

* A 3-way merges use a dedicated commit to tie together the two histories.
* Git uses three commits to generate the merge commit: the two branch tips and their common ancestor.
* This is a common scenario for large features or when several developers are working on a project simultaneously.

<p align="center">
  <img src="https://user-images.githubusercontent.com/90503660/134101319-849370e7-0525-474a-9553-d614c0b7e445.png"> 
</p>

```
### VERIFY THE COMMIT HISTORY TO SEE THE CURRENT STATUS

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git log --oneline
afaf55f (HEAD -> master) second commit
cc9cab9 first commit

### CREATE A NEW FEATURE BRANCH "new-feature" 

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git checkout -b new-feature master
Switched to a new branch 'new-feature'

### UPDATE SOME FILE AND DO A COMMIT

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ vi test

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git status
On branch new-feature
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test

no changes added to commit (use "git add" and/or "git commit -a")

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git add .

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git status
On branch new-feature
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git commit -m "third commit"
[new-feature 523551e] third commit
 1 file changed, 1 insertion(+)

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git status
On branch new-feature
nothing to commit, working tree clean

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git log --oneline
523551e (HEAD -> new-feature) third commit
afaf55f (master) second commit
cc9cab9 first commit

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$

### CHECKOUT TO MASTER AND PERFORM ANOTHER FILE CHANGE & COMMIT

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (new-feature)
$ git checkout master
Switched to branch 'master'

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git status
On branch master
nothing to commit, working tree clean

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git log --oneline
afaf55f (HEAD -> master) second commit
cc9cab9 first commit

### CREATE A NEW FILE IN MASTER BRANCH & COMMIT IT

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ vi file2

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file2

nothing added to commit but untracked files present (use "git add" to track)

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git add .
warning: LF will be replaced by CRLF in file2.
The file will have its original line endings in your working directory

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   file2


klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git commit -m "fourth commit"
[master 2ba32d7] fourth commit
 1 file changed, 1 insertion(+)
 create mode 100644 file2

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git status
On branch master
nothing to commit, working tree clean

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$

### VERIFY THE COMMIT HISTORY, YOU COULD NOT SEE THE "third commit" OF FEATURE BRANCH HERE AS IT IS STILL NOT MERGED TO MASTER.

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git log --oneline
2ba32d7 (HEAD -> master) fourth commit
afaf55f second commit
cc9cab9 first commit

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$

### MERGE THE FEATURE BRANCH CHANGES TO MASTER

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git status
On branch master
nothing to commit, working tree clean

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git merge new-feature
Merge made by the 'recursive' strategy.
 test | 1 +
 1 file changed, 1 insertion(+)

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git status
On branch master
nothing to commit, working tree clean

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git log --oneline
ed2cd74 (HEAD -> master) Merge branch 'new-feature'
2ba32d7 fourth commit
523551e (new-feature) third commit
afaf55f second commit
cc9cab9 first commit

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$

### HERE YOU COULD SEE THE "third commit" ON "new-feature" BRANCH AND A NEW MERGE COMMIT "ed2cd74" HAS BEEN CREATED RATHER THAN A FAST FORWARD COMMIT.
### THIS REQUIRES A 3-WAY MERGE BECAUSE "master" PROGRESSES WHILE THE FEATURE IS IN-PROGRESS. THIS IS A COMMON SCENARIO FOR LARGE FEATURES OR WHEN SEVERAL DEVELOPERS ARE WORKING ON A PROJECT SIMULTANEOUSLY.

### NOW, DELETE THE FEATURE BRANCH "new-feature"

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git branch
* master
  new-feature

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git branch -d new-feature
Deleted branch new-feature (was 523551e).

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git branch
* master

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$ git status
On branch master
nothing to commit, working tree clean

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/test (master)
$


```
