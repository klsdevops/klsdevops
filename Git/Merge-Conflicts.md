# Creating a merge conflict

```

###Create a new directory named git-merge-test, change to that directory, and initialize it as a new Git repo.

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop
$ mkdir git-merge-test

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop
$ cd git-merge-test/

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test
$ git init .
Initialized empty Git repository in C:/Users/sujith/Desktop/git-merge-test/.git/

###Create a new text file merge.txt with some content in it.  

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ echo "this is some content to mess with" > merge.txt

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        merge.txt

nothing added to commit but untracked files present (use "git add" to track)

###Add merge.txt to the repo and commit it.

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git add merge.txt
warning: LF will be replaced by CRLF in merge.txt.
The file will have its original line endings in your working directory

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   merge.txt


klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git commit -am "initial commit"
[master (root-commit) 3414689] initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 merge.txt

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git status
On branch master
nothing to commit, working tree clean

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$

###Now we have a new repo with one branch main and a file merge.txt with content in it

###create a new branch to use as the conflicting merge.

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git checkout -b new_branch_to_merge_later
Switched to a new branch 'new_branch_to_merge_later'

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (new_branch_to_merge_later)
$ echo "totally different content to merge later" > merge.txt

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (new_branch_to_merge_later)
$ cat merge.txt
totally different content to merge later

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (new_branch_to_merge_later)
$ git commit -am"edited the content of merge.txt to cause a conflict"
warning: LF will be replaced by CRLF in merge.txt.
The file will have its original line endings in your working directory
[new_branch_to_merge_later 50581cb] edited the content of merge.txt to cause a conflict
 1 file changed, 1 insertion(+), 1 deletion(-)

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (new_branch_to_merge_later)
$

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (new_branch_to_merge_later)
$ git status
On branch new_branch_to_merge_later
nothing to commit, working tree clean

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (new_branch_to_merge_later)
$ git log --oneline
50581cb (HEAD -> new_branch_to_merge_later) edited the content of merge.txt to cause a conflict
3414689 (master) initial commit

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (new_branch_to_merge_later)
$

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (new_branch_to_merge_later)
$ git checkout master
Switched to branch 'master'

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git log --oneline
3414689 (HEAD -> master) initial commit

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ echo "content to append" >> merge.txt

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ cat merge.txt
this is some content to mess with
content to append

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git commit -am"appended content to merge.txt"
warning: LF will be replaced by CRLF in merge.txt.
The file will have its original line endings in your working directory
[master de2f8a0] appended content to merge.txt
 1 file changed, 1 insertion(+)

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git log --oneline
de2f8a0 (HEAD -> master) appended content to merge.txt
3414689 initial commit

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$

###Merge new_branch_to_merge_later to main
###It will produce a merge conflict now

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git merge new_branch_to_merge_later
Auto-merging merge.txt
CONFLICT (content): Merge conflict in merge.txt
Automatic merge failed; fix conflicts and then commit the result.

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$

###How to identify merge conflicts

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   merge.txt

no changes added to commit (use "git add" and/or "git commit -a")

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$

###Print the content of "merge.txt" to see the conflict details,

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$ cat merge.txt
<<<<<<< HEAD
this is some content to mess with
content to append
=======
totally different content to merge later
>>>>>>> new_branch_to_merge_later

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$

##############################################
##   We can see some strange new additions  ##
##                                          ##
##   <<<<<<< HEAD                           ##
##   =======                                ##
##   >>>>>>> new_branch_to_merge_later      ##
##############################################

### Think of these new lines as "conflict dividers". 
### The ======= line is the "center" of the conflict.
### All the content between the center and the <<<<<<< HEAD line is content that exists in the current branch main which the HEAD ref is pointing to.
### Alternatively all content between the center and >>>>>>> new_branch_to_merge_later is content that is present in our merging branch.

### The other way to identify merge conflicts are by using git commands,

###Passing the --merge argument to the git log command will produce a log with a list of commits that conflict between the merging branches.
klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$ git log --merge
commit de2f8a015a1e1f28012bf0516e3582102f4cf66f (HEAD -> master)
Author: klsdevops <kls13092021@gmail.com>
Date:   Tue Sep 21 10:01:56 2021 +0530

    appended content to merge.txt

commit 50581cb5a5f62cd025215e34ed4ba49521820408 (new_branch_to_merge_later)
Author: klsdevops <kls13092021@gmail.com>
Date:   Tue Sep 21 09:59:49 2021 +0530

    edited the content of merge.txt to cause a conflict

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)

###diff helps find differences between states of a repository/files. This is useful in predicting and preventing merge conflicts.

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$ git diff
diff --cc merge.txt
index 8abf0ff,251d87e..0000000
--- a/merge.txt
+++ b/merge.txt
@@@ -1,2 -1,1 +1,6 @@@
++<<<<<<< HEAD
 +this is some content to mess with
 +content to append
++=======
+ totally different content to merge later
++>>>>>>> new_branch_to_merge_later

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$

###How to resolve merge conflicts using the command line
###The most direct way to resolve a merge conflict is to edit the conflicted file.

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$ vi merge.txt
this is some content to mess with
content to append
totally different content to merge later
~
~
~
~
~
~
merge.txt[+] [dos] (10:03 21/09/2021)    

###Once the file has been edited use git add merge.txt to stage the new merged content.
###To finalize the merge create a new commit 

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   merge.txt

no changes added to commit (use "git add" and/or "git commit -a")

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$ git log --oneline
de2f8a0 (HEAD -> master) appended content to merge.txt
3414689 initial commit

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$ git add .

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$ git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        modified:   merge.txt


klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master|MERGING)
$ git commit -m "merged and resolved the conflict in merge.txt"
[master 4a42701] merged and resolved the conflict in merge.txt

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git log --oneline
4a42701 (HEAD -> master) merged and resolved the conflict in merge.txt
de2f8a0 appended content to merge.txt
50581cb (new_branch_to_merge_later) edited the content of merge.txt to cause a conflict
3414689 initial commit

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git status
On branch master
nothing to commit, working tree clean

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$

###Git will see that the conflict has been resolved and creates a new merge commit to finalize the merge.

### Delete the feature branch
klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git branch
* master
  new_branch_to_merge_later

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git branch -d new_branch_to_merge_later
Deleted branch new_branch_to_merge_later (was 50581cb).

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$
klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$ git branch
* master

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/git-merge-test (master)
$

```
