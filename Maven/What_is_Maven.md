# What is Maven?
Maven is a powerful build automation tool which is primarily used for Java based projects. Maven can also be used to build project written in C#, Ruby, Scalar etc.
Maven addresses the below two issues:
* It describes how software is build?
* It describes the dependencies(Third party dependencies). Dependencies are nothing but the libraries or the jar files.
Maven dynamically downloads Java libraries and maven plugins from one or more repositories such as maven central repository and stores them in the local cache. 
This local cache of the downloaded artifacts can also be updated with the artifacts created by the local projects. Public repositories can also be updated.


# Maven Architecture
When ever you specify a dependency in the pom.xml file, maven will look for that file in the central remote repository.
If the dependency is present in the central repository, maven will copy it to the local machine.

![image](https://user-images.githubusercontent.com/90503660/155913066-1e38b092-4b1a-41a3-93e1-4551973f09de.png)

## Repositories:
Maven repositories are physical directories which contain packaged JAR files along with extra meta data about these jar files.
This meta data is in form of POM files which have jar file project information, including what other external dependencies this JAR file has.
These other external dependencies are downloaded transitively into your project and become part of effective pom for the project.

A repository in Maven holds build artifacts and dependencies of varying types.
There are exactly two types of repositories: **local** and **remote**:
The **local** repository is a directory on the computer where Maven runs. It caches remote downloads and contains temporary build artifacts that you have not yet released.
**Remote** repositories refer to any other type of repository, accessed by a variety of protocols such as file:// and https://. 
These repositories might be a truly remote repository set up by a third party to provide their artifacts for downloading (for example, repo.maven.apache.org).
Other "**remote**" repositories may be internal repositories set up on a file or HTTP server within your company, used to share private artifacts between development teams and for releases.
**Local** and **remote** repositories are structured the same way so that scripts can run on either side, or they can be synced for offline use. 
The layout of the repositories is completely transparent to the Maven user, however.

### Local repository
Maven local repository reside in the developer’s machine.
Whenever you run maven goals which require these dependencies, maven will download the dependencies from remote servers and store them into developer’s machine.
By default, Maven create the local repository inside user home directory ie; **/home/USER/.m2** directory.
You can change the location of the local repository in setting.xml file using localRepository tag.
Having stored the dependencies into local machine has two main benefits.
* First, multiple projects can access same artifact so it reduces the storage need.
* Second, as dependency is downloaded only once, it reduces the network usage as well.
  
### Central repository
Maven central repository is located at http://repo.maven.apache.org/maven2/. Whenever you run build job, maven first try to find dependency from local repository. 
If it is not there, then, by default, maven will trigger the download from this central repository location.
To override this default location, you can can make changes to your settings.xml file to use one or more mirrors.
You do not need to make any special configuration to allow access the central repository, except network proxy settings if you are behind any firewall.

### Remote repository
Apart from central repository, you may have needed artifacts deployed on other remote locations. 
For example, in your corporate office there may be projects or modules specific to organization only. 
In this cases, organization can create remote repository and deploy these private artifacts. This remote repository will be accessible only inside organization.
These maven remote repository work exactly same way as maven’s central repository.
Whenever an artifact is needed from these repositories, it is first downloaded to developer’s local repository and then it is used.
You can configure a remote repository in the POM file or super POM file in remote repository itself.
