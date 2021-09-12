# This file contains the things to be considered while working with GIT
## 1. Proxy Configurations
If your organization uses a proxy, you will need to configure the proxy settings in GIT.
You can do it from the command line with the below steps:

  ```$ git config --global http.proxy https://YOUR.PROXY.SERVER:8080```
  
  Replace the YOUR.PROXY.SERVER with your proxy's URL.
  
  If your proxy does require authentication:
  
  ```$ git config --global http.proxy https://YOUR_PROXY_USERNAME:YOUR_PROXY_PASSWORD@YOUR.PROXY.SERVER:8080```
  
  Replace YOUR_PROXY_USERNAME with the username used to authenticate into your proxy, YOUR_PROXY_PASSWORD with the password used to authenticate in to your proxy and YOUR.PROXY.SERVER with your proxy's URL.
  
## 2. Setup your Text Editor:
When you create a Git commit with ``` git commit -a ``` , the default editor that will be opened is vim. This can be changed with respect to the editor what you are comfortable.
You can use almost any text editor, but we have the best success with the following:
  * Atom
  * Visual Studio Code
  * Notepad
  * Vi or Vim
  * Sublime
  * Notepad++
  * Gitpad
  
The command to do this is 

  ``` $ git config --global core.editor nano ```
  
## 3. Force git to use HTTPS.
If you can't clone a repository with a "git://" url because of a proxy or firewall, here is a little git configuration that will force git to use "https://" even when you'll type "git://" URL.

``` $ git config --global url."https://".insteadOf git:// ```

With this command, it will add the following lines in you .gitconfig :

``` 
    [url "https://"]   
    insteadOf = git://
```

This way, you don't have to care about using "git://" or "https://" when you are cloning repo, both urls will work.

This usually happens when you are trying to clone some of the npm repositories.

### How to remove/revert back this to use git://
You can edit the whole global config file by running ``` git config --global --edit ``` and delete the line manually.
OR

``` $ git config --global --unset-all url.https://.insteadof ```

OR

if any anyone need the reverse of this:

``` $ git config --global url."git://".insteadOf https:// ```

## 4. Good commit messages should:
When you commit changes to your repository, the best practice for commit message should be as below;
  * Be short. ~50 characters is ideal.
  * Describe the change Introduced by the commit.
  * Tell the story of how your project has evolved.

## 5. Credential helper settings
When you **push** changes, you will be asked to enter your GitHub username and password. If you would like to remember your credentials on this computer, you can cache your credentials using:
For Windows:

``` $ git config --global credential.helper wincred ```

For newer versions of Git,

``` $ git config --global credential.helper manager-core ```

_Note: You can remove these settings from your window Credential Manager,
      Control Panel -> User Accounts -> Credential Manager -> Windows Credentials -> Generic Credentials
      Edit or Remove the values._
  
