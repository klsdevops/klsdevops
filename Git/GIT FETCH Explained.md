# GIT FETCH EXPLAINED:

To get the changes in the remote origin to local repo without updating your working directory.

## Test scenario:
  1. Make some changes in the remote.
  2. check the commit ID.
  3. perform `git fetch` from the command line
  4. to see the changes, you should go to the **refs/remotes/origin**. Here you could see the remote branches where you have made updates. You could see the latest commit ID here.   
But when you do a git log on your local repo, you can't see the latest commit id until you merge those changes with the 'origin/<branch>'.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Scenario 1: CREATE A NEW BRANCH ON THE REMOTE & UPDATE SOME CHANGES ON FILES.

FROM THE LOCAL REPO, LIST THE BRANCHES(BEFORE FETCH)
	
```
klsdevops (main)$ git branch -a
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main

klsdevops (main)$ ls -ltr
total 1
-rw-r--r-- 1 klsdevops 197121 423 Sep 12 14:25 README.md
drwxr-xr-x 1 klsdevops 197121   0 Sep 12 14:25 Jenkins/
drwxr-xr-x 1 klsdevops 197121   0 Sep 13 23:48 Git/

  ```
  
### VERIFY THE EXISTING REMOTE REFERENCES:

  ```
  
klsdevops (main)$ cd .git/refs/remotes/

klsdevops/.git/refs/remotes (GIT_DIR!)$ ls -ltr
total 0
drwxr-xr-x 1 klsdevops 197121 0 Sep 13 23:46 origin/

klsdevops/.git/refs/remotes (GIT_DIR!)$ cd origin/

  ```
  
### YOU COULD SEE THERE ARE ONLY ONE BRANCH AVAILABLE NOW:

  ```
  
klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ ls -ltr
total 2
-rw-r--r-- 1 klsdevops 197121 30 Sep 12 14:25 HEAD
-rw-r--r-- 1 klsdevops 197121 41 Sep 13 23:46 main

klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ cat HEAD
ref: refs/remotes/origin/main

klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ cat main
67a91827b0c877172f2cf57fd4507fa0a3899929

  ```
  
### VERIFY THE COMMIT ID:

  ```
  
klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ git log
commit 67a91827b0c877172f2cf57fd4507fa0a3899929 (HEAD -> main, origin/main, origin/HEAD)
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:55:14 2021 +0530

    updated credential helper settings

commit b1a419bcfdc6886848db371cafc776fa355ba67e
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:46:04 2021 +0530

    Update Thing to consider.md
	
klsdevops/.git/refs/remotes/origin (GIT_DIR!)$

  ```
  
### PERFORM A GIT FETCH TO DOWNLOAD THE CHANGES TO LOCAL REPO:

  ```
  
klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ cd -

klsdevops (main)$ git fetch
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 667 bytes | 2.00 KiB/s, done.
From https://github.com/klsdevops/klsdevops
 * [new branch]      test       -> origin/test

  ```
  
### NOW YOU COULD SEE THE NEW REMOTE BRANCH HAS BEEN DOWNLOADED TO LOCAL REPO

  ```
  
klsdevops (main)$ git branch -a
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
  remotes/origin/test

klsdevops (main)$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean

  ```
  
### GO TO THE REMOTE REFERENCES AND SEE THE UPDATES:

  ```
klsdevops (main)$ cd .git/refs/remotes/origin/

klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ ls -ltr
total 3
-rw-r--r-- 1 klsdevops 197121 30 Sep 12 14:25 HEAD
-rw-r--r-- 1 klsdevops 197121 41 Sep 13 23:46 main
-rw-r--r-- 1 klsdevops 197121 41 Sep 14 07:36 test

  ```
  
### YOU ARE ABLE TO SEE THE NEW BRANCH UPDATED HERE.

  ```
  
klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ cat test
d41ff2964a7fb5db84f12ab00767529c297ceb57

  ```
  
### YOU COULD SEE THE LATEST COMMIT ID ON THAT REMOTE BRANCH.
### BUT IF YOU VERIFY YOUR main BRANCH COMMIT, IT REMAINS THE SAME BECAUSE THE CHANGES WERE DONE ON THE REMOTE FEATURE BRANCH ("test").

  ```
  
klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ cd -

klsdevops (main)$ git log
commit 67a91827b0c877172f2cf57fd4507fa0a3899929 (HEAD -> main, origin/main, origin/HEAD)
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:55:14 2021 +0530

    updated credential helper settings

commit b1a419bcfdc6886848db371cafc776fa355ba67e
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:46:04 2021 +0530

    Update Thing to consider.md

  ```
  
### TO SEE THE CHANGES ON THE FEATURE BRANCH, YOU NEED TO SWITCH TO THAT BRANCH:

  ```
  
klsdevops (main)$ git checkout test
Switched to a new branch 'test'
Branch 'test' set up to track remote branch 'test' from 'origin'.

  ```
  
### IF YOU CHECK THE STATUS, YOU COULD SEE ITS UP TO DATE.

  ```
  
klsdevops (test)$ git status
On branch test
Your branch is up to date with 'origin/test'.

nothing to commit, working tree clean

klsdevops (test)$

  ```
  
### VERIFY THE COMMIT ID:

  ```
  
klsdevops (test)
$ git log
commit d41ff2964a7fb5db84f12ab00767529c297ceb57 (HEAD -> test, origin/test)
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Tue Sep 14 07:34:10 2021 +0530

    test fetch added

commit 67a91827b0c877172f2cf57fd4507fa0a3899929 (origin/main, origin/HEAD, main)
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:55:14 2021 +0530

    updated credential helper settings

commit b1a419bcfdc6886848db371cafc776fa355ba67e
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:46:04 2021 +0530

    Update Thing to consider.md

klsdevops (test)$ cd -
klsdevops/.git/refs/remotes/origin

klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ cat test
d41ff2964a7fb5db84f12ab00767529c297ceb57

  ```
  
### THE LATEST COMMIT IDs ARE THE REFLECTED. DURING THE INITIAL CHECKOUT "Branch 'test' set up to track remote branch 'test' from 'origin'". BUT FROM THE SUBSEQUENT UPDATES ONWARDS, YOU WILL HAVE TO PERFORM A SEPARATE MERGE TO REFLECT THE REMOTE CONTENTS ON THE WORKING DIRECTORY. WHICH WILL BE EXPLAINED IN THE NEXT SCENARIO.

## SCENARIO 2:  WHERE SOME UPDATES PERFORMED ON THE EXISTING REMOTE FEATURE BRANCH :

### MAKE SOME CHANGES ON THE REMOTE FEATURE BRANCH "test"

### AFTER MAKING THE CHANGES ON THE REMOTE, CHECK THE FILE CONTENT ON YOU WORKING DIRECTORY(BEFORE FETCH). [OFCOURSE YOU CAN NOT SEE ANY CHANGES FROM THE REMOTE TO LOCAL]

  ```
  
klsdevops (test)$ cat README.md
- 👋 Hi, I’m @klsdevops
- 👀 I’m interested in continuous learning
- 🌱 I’m currently learning DevOps
- 💞️ I’m looking to collaborate on DevOps Practices
- 📫 How to reach me kls13092021@gmail.com

<!---
klsdevops/klsdevops is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

Test fetch

  ```
  
### VERIFY THE STATUS & COMMIT IDs:

  ```
  
klsdevops (test)$ git status
On branch test
Your branch is up to date with 'origin/test'.

nothing to commit, working tree clean

klsdevops (test)$ git log
commit d41ff2964a7fb5db84f12ab00767529c297ceb57 (HEAD -> test, origin/test)
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Tue Sep 14 07:34:10 2021 +0530

    test fetch added

commit 67a91827b0c877172f2cf57fd4507fa0a3899929 (origin/main, origin/HEAD, main)
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:55:14 2021 +0530

    updated credential helper settings

commit b1a419bcfdc6886848db371cafc776fa355ba67e
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:46:04 2021 +0530

    Update Thing to consider.md

  ```
  
### VERIFY THE REMOTE REFERENCES CONTENT AS WELL:

  ```
  
klsdevops (test)$ cd -
klsdevops/.git/refs/remotes/origin

klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ cat test
d41ff2964a7fb5db84f12ab00767529c297ceb57

  ```
  
### ALSO VERIFFY THE CHANGES ON YOUR OWN LOCAL BRANCHES UNDER "ref/heads". 

  ```
  
klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ cd ../../heads

klsdevops/.git/refs/heads (GIT_DIR!)$ ls -ltr
total 2
-rw-r--r-- 1 klsdevops 197121 41 Sep 13 23:48 main
-rw-r--r-- 1 klsdevops 197121 41 Sep 14 07:41 test

klsdevops/.git/refs/heads (GIT_DIR!)$ cat test
d41ff2964a7fb5db84f12ab00767529c297ceb57

  ```
  
### THE COMMIT ID WILL BE THE SAME AS OF NOW.

  ```
  
klsdevops/.git/refs/heads (GIT_DIR!)$ cd ../remote/origin

  ```
  
### NOW PERFORM A GIT FETCH TO DOWNLOAD THE CHANGES TO LOCAL REPO:

  ```
  
klsdevops (test)$ git fetch
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 670 bytes | 4.00 KiB/s, done.
From https://github.com/klsdevops/klsdevops
   d41ff29..9b82215  test       -> origin/test

  ```
  
### VERIFY THE COMMIT ID ON YOUR LOCAL. YOU CAN NOTICE, THE COMMIT ID IS NOT UPDATED EVEN AFTER THE DOWNLOAD(FETCH).

  ```
  
klsdevops (test)$ git log
commit d41ff2964a7fb5db84f12ab00767529c297ceb57 (HEAD -> test)
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Tue Sep 14 07:34:10 2021 +0530

    test fetch added

commit 67a91827b0c877172f2cf57fd4507fa0a3899929 (origin/main, origin/HEAD, main)
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:55:14 2021 +0530

    updated credential helper settings

commit b1a419bcfdc6886848db371cafc776fa355ba67e
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:46:04 2021 +0530

    Update Thing to consider.md

  ```
  
### BUT NOW IF YOU GO TO THE GIT REMOTE REFERENCES, YOU COULD SEE THE LATEST COMMIT ID IS UPDATED THERE.

  ```
  
klsdevops (test)$ cd -
klsdevops/.git/refs/remotes/origin

klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ cat test
9b8221574c7503e389b67d03655317c5d7985b2f

klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ ls -tlr
total 3
-rw-r--r-- 1 klsdevops 197121 30 Sep 12 14:25 HEAD
-rw-r--r-- 1 klsdevops 197121 41 Sep 13 23:46 main
-rw-r--r-- 1 klsdevops 197121 41 Sep 14 07:39 test

klsdevops/.git/refs/remotes (GIT_DIR!)$ cd -

  ```
  
### VERIFY THE CONTENT OF THE FILE CHANGED, YOU WILL NOTICE THERE ARE NO CHANGES DOWNLOADED ON TO YOUR WORKING DIRECTORY.

  ```
  
klsdevops (test)$ cat README.md
- 👋 Hi, I’m @klsdevops
- 👀 I’m interested in continuous learning
- 🌱 I’m currently learning DevOps
- 💞️ I’m looking to collaborate on DevOps Practices
- 📫 How to reach me kls13092021@gmail.com

<!---
klsdevops/klsdevops is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

Test fetch

  ```
  
### NOW IF YOU VERIFY THE CHANGES ON YOUR OWN LOCAL BRANCHES UNDER "refs/heads" YOU COULD SEE THE LATEST COMMIT ID IS NOT UPDATED THERE AS WELL.

  ```
  
klsdevops (test)$ cd .git/refs/heads
klsdevops/.git/refs/heads (GIT_DIR!)$ ls -ltr
total 2
-rw-r--r-- 1 klsdevops 197121 41 Sep 13 23:48 main
-rw-r--r-- 1 klsdevops 197121 41 Sep 14 07:41 test

klsdevops/.git/refs/heads  (GIT_DIR!)$ cat test
d41ff2964a7fb5db84f12ab00767529c297ceb57

  ```
  
### HOW CAN WE BRING THE CHANGES FROM THE WORKING DIRECTORY TO LOCAL ? FOR THIS, WE NEED TO PERFORM A MERGE ACTIVITY.

  ```
  
klsdevops (test)$ git status
On branch test
Your branch is behind 'origin/test' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean

klsdevops (test)$ git merge origin/test
Updating d41ff29..9b82215
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)

  ```
  
### NOW IF YOU VERIFY THE CONTENT OF THE FILE CHANGED, YOU COULD SEE THE LATEST UPDATES IN YOUR WORKING DIRECTORY.

  ```
  
klsdevops (test)$ cat README.md
- 👋 Hi, I’m @klsdevops
- 👀 I’m interested in continuous learning
- 🌱 I’m currently learning DevOps
- 💞️ I’m looking to collaborate on DevOps Practices
- 📫 How to reach me kls13092021@gmail.com

<!---
klsdevops/klsdevops is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

Test fetch
another edit

 klsdevops (test)$ 

  ```
  
### ALSO WHEN YOU CHECK THE COMMIT ID, YOU COULD SEE THE LATEST COMMIT ID IS ALSO UPDATED THERE.

  ```
  
klsdevops (test)$ git status
On branch test
Your branch is up to date with 'origin/test'.

nothing to commit, working tree clean

klsdevops (test)$ git log
commit 9b8221574c7503e389b67d03655317c5d7985b2f (HEAD -> test, origin/test)
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Tue Sep 14 07:38:32 2021 +0530

    Update README.md

commit d41ff2964a7fb5db84f12ab00767529c297ceb57
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Tue Sep 14 07:34:10 2021 +0530

    test fetch added

commit 67a91827b0c877172f2cf57fd4507fa0a3899929 (origin/main, origin/HEAD, main)
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:55:14 2021 +0530

    updated credential helper settings

commit b1a419bcfdc6886848db371cafc776fa355ba67e
Author: klsdevops <90503660+klsdevops@users.noreply.github.com>
Date:   Sun Sep 12 15:46:04 2021 +0530

    Update Thing to consider.md

klsdevops (test)$

klsdevops (test)$ cd .git/refs/remotes/origin/

klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ ls -ltr
total 3
-rw-r--r-- 1 klsdevops 197121 30 Sep 12 14:25 HEAD
-rw-r--r-- 1 klsdevops 197121 41 Sep 13 23:46 main
-rw-r--r-- 1 klsdevops 197121 41 Sep 14 07:39 test

klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ cat test
9b8221574c7503e389b67d03655317c5d7985b2f

klsdevops/.git/refs/remotes/origin (GIT_DIR!)$

  ```
  
### IF YOU CHECK THE COMMIT ID ON YOUR OWN LOCAL BRANCH, YOU COULD SEE THAT'S ALSO UPDATED WITH LATEST NOW.

  ```
  
klsdevops/.git/refs/remotes/origin (GIT_DIR!)$ cd ../../heads/

klsdevops/.git/refs/heads (GIT_DIR!)$ ls -ltr
total 2
-rw-r--r-- 1 klsdevops 197121 41 Sep 13 23:48 main
-rw-r--r-- 1 klsdevops 197121 41 Sep 14 07:41 test

klsdevops/.git/refs/heads (GIT_DIR!)$ cat test
9b8221574c7503e389b67d03655317c5d7985b2f

klsdevops/.git/refs/heads (GIT_DIR!)$

  ```
  
**NOTE**: _If multiple branches are updated in the remote & we do a fetch from local, all the changes will be downloaded to local repo. But in order to get it reflected in the local branches and working directory, you will have to perform merge with each **remote->local** branches._

	
## While doing a git fetch you could see the difference & decide if you want to proceed with a merge or not,

### 1. Before bringing changes from remote, see the diff:
![image](https://user-images.githubusercontent.com/90503660/133364623-229faa90-4bb3-4e14-b72a-7cd50df08197.png)

### 2. make some changes in remote
![image](https://user-images.githubusercontent.com/90503660/133365464-a93c2549-1e03-4efe-aab8-2b9591940467.png)
	
### 3. After fetching the remote changes, again see the diff:
![image](https://user-images.githubusercontent.com/90503660/133364885-576f8741-e88e-4c39-b1c6-7375c401bb80.png)

You could see the line added with a "+" symbol in GREEN colour.

### 4. if you are happy with the updates, you can merge those changes.
	
