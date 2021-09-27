# What is in .git ?
A git repository is a collection of all project files along with their history.
So when you initiate a git repository, the ".git" folder is getting created and it is used by GIT programs to store information about the repository like logs, position of HEAD, commits, etc.

### Create a directory & initiate it as a git repository

```
klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop
$ mkdir dot-git

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop
$ cd dot-git/

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git
$ ls -ltra
total 16
drwxr-xr-x 1 klsdevops 197121 0 Sep 24 06:18 ../
drwxr-xr-x 1 klsdevops 197121 0 Sep 24 06:18 ./

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git
$

```

### The moment you make this directory/folder as a git repository, you can see a "._git_" folder has been created in it.

```

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git
$ git init
Initialized empty Git repository in C:/Users/klsdevops/Desktop/dot-git/.git/

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
$ ls -ltra
total 20
drwxr-xr-x 1 klsdevops 197121 0 Sep 24 06:18 ../
drwxr-xr-x 1 klsdevops 197121 0 Sep 24 06:19 ./
drwxr-xr-x 1 klsdevops 197121 0 Sep 24 06:19 .git/

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
$

```

### Now let's see what's inside ._git_ folder

```
klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
$ cd .git/

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git (GIT_DIR!)
$ ls -ltra
total 11
drwxr-xr-x 1 klsdevops 197121   0 Sep 24 06:19 refs/
drwxr-xr-x 1 klsdevops 197121   0 Sep 24 06:19 info/
drwxr-xr-x 1 klsdevops 197121   0 Sep 24 06:19 hooks/
-rw-r--r-- 1 klsdevops 197121  73 Sep 24 06:19 description
-rw-r--r-- 1 klsdevops 197121  23 Sep 24 06:19 HEAD
drwxr-xr-x 1 klsdevops 197121   0 Sep 24 06:19 ../
drwxr-xr-x 1 klsdevops 197121   0 Sep 24 06:19 objects/
-rw-r--r-- 1 klsdevops 197121 130 Sep 24 06:19 config
drwxr-xr-x 1 klsdevops 197121   0 Sep 24 06:19 ./

klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git (GIT_DIR!)
$

```

**1.** **HEAD file in .git folder**

          Head file contains the reference to the branch we are currently working on(currently active branch). 
          It is a symbolic reference to the branch, something like a pointers in programming.
          A normal reference contain the HASH value(SHA-1).
          A symbolic reference is a reference to another normal reference.
          We will see what it means;
          
          If you browse through the other files and folders, you could see a "refs" folder which contains the normal references.
          
          ```
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git/refs (GIT_DIR!)
          $ ls -ltr
          total 0
          drwxr-xr-x 1 klsdevops 197121 0 Sep 24 06:19 tags/
          drwxr-xr-x 1 klsdevops 197121 0 Sep 24 06:19 heads/

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git/refs (GIT_DIR!)
          $

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git (GIT_DIR!)
          $ cd heads/

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git/refs/heads (GIT_DIR!)
          $ ls -ltr
          total 0

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git/refs/heads (GIT_DIR!)
          $
          
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git log
          fatal: your current branch 'master' does not have any commits yet

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $

          ```
          
          INITIALLY, THERE ARE NO FILES AVAILABLE UNDER /refs/
          NOW LET'S ADD SOME FILES AND COMMIT TO THE REPOSITORY
          
          ```
          
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ ls -ltr
          total 0

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ echo "this is a dummy file" > dummy.txt

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ ls -ltr
          total 1
          -rw-r--r-- 1 klsdevops 197121 21 Sep 24 06:35 dummy.txt

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cat dummy.txt
          this is a dummy file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $
          
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git add .
          warning: LF will be replaced by CRLF in dummy.txt.
          The file will have its original line endings in your working directory

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git commit -m "created dummy file"
          [master (root-commit) e939194] created dummy file
           1 file changed, 1 insertion(+)
           create mode 100644 dummy.txt

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git log
          commit e9391940d632e9417730081fb838e9ec005dfb1f (HEAD -> master)
          Author: klsdevops <kls13092021@gmail.com>
          Date:   Fri Sep 24 06:36:46 2021 +0530

              created dummy file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $

          ```
          
          NOW, LET'S GO BACK TO THE ".git/refs/head" FOLDER AND SEE THE REFERENCES CREATED THERE.
          
          ```
          
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cd .git/refs/heads/

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git/refs/heads (GIT_DIR!)
          $ ls -ltr
          total 1
          -rw-r--r-- 1 klsdevops 197121 41 Sep 24 06:36 master

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git/refs/heads (GIT_DIR!)
          $ cat master
          e9391940d632e9417730081fb838e9ec005dfb1f

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git/refs/heads (GIT_DIR!)
          $
          
          ```
          
          YOU COULD SEE A NEW FILE "master" HAS BEEN CREATED & IT CONTAIN A COMMIT REFERENCE TO THE LATEST COMMIT WHERE THE SYMBOLIC REFERENCE "HEAD" IS POINTING TO.
          
          NOW VERIFY THE CONTENTS OF "HEAD". YOU WILL SEE, THE "HEAD" SAYS A REFERENCE POINTER TO THE ACTUAL REFERENCE FILE.
          
          ```
          
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git/refs/heads (GIT_DIR!)
          $ cd ../..

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git (GIT_DIR!)
          $ cat HEAD
          ref: refs/heads/master

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git (GIT_DIR!)
          $
          
          ```
          
          IF YOU WANT TO SEE THE DIFFERENCE, WE WILL CREATE A NEW BRANCH & SEE WHAT HAPPENS.
          
          ```
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git/.git (GIT_DIR!)
          $ cd ..

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git branch new-branch

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git branch
          * master
            new-branch

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ ls -ltr .git/refs/heads/
          total 2
          -rw-r--r-- 1 klsdevops 197121 41 Sep 24 06:36 master
          -rw-r--r-- 1 klsdevops 197121 41 Sep 24 06:43 new-branch

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cat .git/refs/heads/new-branch
          e9391940d632e9417730081fb838e9ec005dfb1f

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cat .git/refs/heads/master
          e9391940d632e9417730081fb838e9ec005dfb1f

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cat .git/HEAD
          ref: refs/heads/master

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $
          
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git log
          commit e9391940d632e9417730081fb838e9ec005dfb1f (HEAD -> new-branch, master)
          Author: klsdevops <kls13092021@gmail.com>
          Date:   Fri Sep 24 06:36:46 2021 +0530

            created dummy file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $
          ```
          
          HERE YOU COULD SEE THAT THE BRANCH "new-branch" HAS BEEN CREATED BASED ON "master" BRANCH AND HENCE IT ALSO HAVE THE SAME MASTER COMMIT HASH(SHA-1) ON IT NOW.

          NOW SWITCH TO THE "new-branch" AND SEE THE POSITION OF HEAD
          
          ```
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git checkout new-branch
          Switched to branch 'new-branch'

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ cat .git/HEAD
          ref: refs/heads/new-branch

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $
          
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ git log
          commit e9391940d632e9417730081fb838e9ec005dfb1f (HEAD -> new-branch, master)
          Author: klsdevops <kls13092021@gmail.com>
          Date:   Fri Sep 24 06:36:46 2021 +0530

            created dummy file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $
          
          ```
          YOU ARE SEEING THE HEAD IS NOW POINTING TO THE "new-branch" REERENCES AS WELL. 
          LET'S SEE WHAT'S THE NORMAL REFERENCE FOR THE "new-branch"
          
          ```
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ cat .git/refs/heads/new-branch
          e9391940d632e9417730081fb838e9ec005dfb1f

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $
          
          ```
          
          AS OF NOW IT HAVE ONLY THE COMMIT FROM MASTER AND ITS POINTING TO THAT COMMIT REFERENCE. 
          IF YOU CHECK THE REFERENCE OF "master" BRANCH ALSO, YOU WILL SEE THE SAME COMMIT HASH FOR NOW.
          
          ```
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ cat .git/refs/heads/master
          e9391940d632e9417730081fb838e9ec005dfb1f

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $

          ```

          NOW LET'S MAKE SOME CHANGES ON THE "new-branch" AND DO A NEW COMMIT TO IT & VERIFY THE HEAD & REFERENCES,
          
          ```
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ echo "contents of file in feature branch" > new-branch-file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ git status
          On branch new-branch
          Untracked files:
            (use "git add <file>..." to include in what will be committed)
                  new-branch-file

          nothing added to commit but untracked files present (use "git add" to track)

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ git add .
          warning: LF will be replaced by CRLF in new-branch-file.
          The file will have its original line endings in your working directory

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ git commit -m "added feature file"
          [new-branch 313a15c] added feature file
           1 file changed, 1 insertion(+)
           create mode 100644 new-branch-file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ git log
          commit 313a15c8db563a510849fae4b6ddd8f9fca693fc (HEAD -> new-branch)
          Author: klsdevops <kls13092021@gmail.com>
          Date:   Fri Sep 24 06:52:58 2021 +0530

              added feature file

          commit e9391940d632e9417730081fb838e9ec005dfb1f (master)
          Author: klsdevops <kls13092021@gmail.com>
          Date:   Fri Sep 24 06:36:46 2021 +0530

              created dummy file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $

          ```
          
          NOW YOU SEE A NEW COMMIT FOR THE "new-branch". LET'S CHECK THE REFERENCES AND SEE THE DIFFERENCE.
          
          ```
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ cat .git/HEAD
          ref: refs/heads/new-branch

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ cat .git/refs/heads/new-branch
          313a15c8db563a510849fae4b6ddd8f9fca693fc

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $

          ```
          
          YOU CAN SEE THE SYMBOLIC REFERENCE (HEAD) IS POINTING TO THE "new-branch" REFERENCE & IF YOU CHECK THE CONTENTS, 
          IT HAS THE COMMIT ID OF THE LATEST COMMIT OF "new-branch". THE MASTER BRANCH COMMIT WILL HAVE DIFFERENT VALUE
          
          ```
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ cat .git/refs/heads/master
          e9391940d632e9417730081fb838e9ec005dfb1f

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ git log --oneline
          313a15c (HEAD -> new-branch) added feature file
          e939194 (master) created dummy file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $
          
          ```
          
          SO IDEALLY THE "HEAD" FILE WILL SHOW A SYMBOLIC REFERENCE TO YOUR CURRENT ACTIVE BRANCH REFERENCE.
          
          WHEN YOU CHECKOUT BACK TO MASTER BRANCH, YOU CAN SEE THE VALUE OF "HEAD" FILE IS CHANGING BACK TO MASTER BRANCH REFERENCE,
          
          ```
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ git checkout master
          Switched to branch 'master'

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cat .git/HEAD
          ref: refs/heads/master

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $
          
          ```
          
          NOW WHEN YOU DO A MERGE AND CHECK THE REFERENCES, YOU WILL NOTICE THE REFERENCE OF BOTH BRANCHES HAVE THE SAME SHA-1 COMMIT VALUE,
          
          ```
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git merge new-branch
          Updating e939194..313a15c
          Fast-forward
           new-branch-file | 1 +
           1 file changed, 1 insertion(+)
           create mode 100644 new-branch-file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git log --oneline
          313a15c (HEAD -> master, new-branch) added feature file
          e939194 created dummy file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cat .git/HEAD
          ref: refs/heads/master

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cat .git/refs/heads/master
          313a15c8db563a510849fae4b6ddd8f9fca693fc

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cat .git/refs/heads/new-branch
          313a15c8db563a510849fae4b6ddd8f9fca693fc

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $
          
          ```
          NOW LET'S GUESS AFTER SO MANY NEW OTHER COMMITS, LETS CHECK THE POSITION OF HEAD FOR EACH BRANCHES. 
          WHEN YOU ARE ON MASTER BRANCH, YOU CAN SEE THE COMMIT HISTORY AND NOTICE THE HEAD REFERENCE IS ON THE LATEST COMMIT OF MASTER BRANCH.
          BUT WHEN YOU SWITCH TO THE "new-branch" YOU COULD SEE THE HEAD IS REFERENCING TO THE LATEST COMMIT OF "new-branch"
          
          ```
          
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git log --oneline
          e815f7a (HEAD -> master) conflict resolved
          ab4b2c9 modified dummy file from master
          a0c91ff (new-branch) modified the same dummy file from new branch
          ba330bf modified for conflict
          313a15c added feature file
          e939194 created dummy file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cat .git/HEAD
          ref: refs/heads/master

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cat .git/refs/heads/master
          e815f7aa79414517e2f74332ab29d141ee06eb3e

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ cat .git/refs/heads/new-branch
          a0c91ff649d880db375fa9f0a237815361d57f06

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git checkout new-branch
          Switched to branch 'new-branch'

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ cat .git/HEAD
          ref: refs/heads/new-branch

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $ git log --oneline
          a0c91ff (HEAD -> new-branch) modified the same dummy file from new branch
          313a15c added feature file
          e939194 created dummy file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (new-branch)
          $
          
          ```
          
**2. The ".git/refs" folder**
          
          References are stored in subdirectories of this directory.
          
          _refs/heads/<branch-name>_
            records tip-of-the-tree commit objects of branch name

          _refs/tags/<name>_
            Each file corresponds to the tag previously created using the git tag command. Its content is nothing but a hash commit attached to the tag.

          _refs/remotes/<branch-name>_
            records tip-of-the-tree commit objects of branches copied from a remote repository.
           
**3. Config File**
 
          All the configurations set to your repository will be saved here.
          Its a repository specific configuration file. 
          These are the repository level configurations. They only apply to the specific repository where they are set.
          
**4. Object folder**
  
          This is an important folder where every commit, every tree or every file that you create is being saved.
          With every object, there is a hash value linked to it, through which Git knows where is what.
          These contain the hash value of the events you did. Git tracks and recognizes everything by converting it to the hash value.
          
**5. Info Folder**

          Additional information about the repository is recorded in this directory.
          "Info" folder contains the "exclude" file inside it. As the name suggests, "exclude file" is used for excluding some specific patterns in the code that you don't want Git to read or execute as to say.
          **Remember that this file is local and personal to you and is not shared among the developers that clone your project.**
          We have another file called ".gitignore" which should be used by all the developers to exclude/ignore files.
          
**6. Logs**

          Records of changes made to refs are stored in this directory. 
          logs/refs/heads/<name>
            Records all changes made to the branch tip named <name>.

          logs/refs/tags/<name>
            Records all changes made to the tag named <name>.
  
**7. Hooks**

          Hooks are customization scripts used by various Git commands. 
          A handful of sample hooks are installed when git init is run, but all of them are disabled by default. To enable, the .sample suffix has to be removed from the filename by renaming.
          Git hooks are the scripts that are executed before or after the events. These events can be any Git event including the common Git events like commit, push, or receive. 
  
**8. Index**

          The current index file for the repository. It is usually not found in a bare repository.
          The index is one of the most important data structures in git.
          It represents a virtual working tree state by recording list of paths and their object names and serves as a staging area to write out the next tree object to be committed.
          Git index file (.git/index) is a binary file having the following format: a 12-byte header, a number of sorted index entries, extensions, and a SHA-1 checksum. 
          git ls-files can show you the contents of the index:
          
          ```
          
          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)
          $ git ls-files --stage
          100644 438bcd7e8944677b63943561cd7165ebc73183b6 0       dummy.txt
          100644 df881c0a519bc9e70b0b9c1e3a2e7d802c57d4ae 0       new-branch-file

          klsdevops@DESKTOP-IPOC5HT MINGW64 ~/Desktop/dot-git (master)

          ```
           
          The flag --stage shows staged contents’ mode bits, object name and stage number in the output.
          So in our case, the output means:

            * The file mode bits are 100644, a regular non-executable file. Mode bits, the 6 digits, is the octal notation of the file permission.
            * The SHA-1 value of blob dummy.txt & new-branch-file.
            * The stage number (slots), useful during merge conflict handling.
            * The object name.
          
          The different stage numbers are not really used during git-add command. They are used for handling merge conflicts. In a nutshell:

            * Slot 0: “normal”, un-conflicted, all-is-well entry.
            * Slot 1: “base”, the common ancestor version.
            * Slot 2: “ours”, the target (HEAD) version.
            * Slot 3: “theirs”, the being-merged-in version.
  
  
  ### Deleting a ._git_ folder
  
  Deleting this folder deletes your entire history. And hence your repository will no longer be available. Though your project source code files are still available inside the project folder, the git history will be completely erased & you can not get the history through the git commands.
