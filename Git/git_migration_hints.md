# Some hints on migration activity from GITLAB to Azure Repos:

* First create a repository in Target environment (eg; Azure Repos)
* Then do a bare clone of the source repository using below command in a staging area(can be your laptop)

`
$ git clone --bare https://<GITHUB_DOMAIN>.com/<USER>/<REPO_NAME>.git
`

When you use the --bare parameter with git clone, you’ll get a copy of the remote repository with no working directory.
This indicates that a repository will be created with the project’s history, which may be pushed and pulled from but not directly modified.
Furthermore, with the --bare repository, no remote branches for the repo will be enabled.
This is a bare repo meant only for migration.
It is not the local repo for interacting with the migrated repository in Azure Repos.
    
* Push the locally cloned repository to Target(Azure Repos) using the “mirror” option

`
$ cd <REPO_NAME>.git
$ git push --mirror https://vsts.com/<USERNAME>/<REPOSITORY>.git
`

This guarantees that any references to the imported repository, such as branches and tags, are copied.
		
*Note:* This activity can be done manually or it can be done through some automated scripts if we are migrating 100s of repositories.

## Lets try the basic steps for migrating a repo from GITHUB to Azure Repos

### Create a target repository in the Azure DevOps 

![image](https://user-images.githubusercontent.com/90503660/154623476-ea730edb-7ecc-4fb1-a24d-53577b93b71e.png)

### do a bare clone of the source repository using below command in a staging area(can be your laptop)
`
git clone --bare https://github.com/klsdevops/banking-repo.git
`

![image](https://user-images.githubusercontent.com/90503660/154623803-103f48b6-dd9c-45c9-ac8e-bfcec75219d6.png)

### Verify the bare cloned repository

Here you could see it didn't bring your working directory, it only brought the history of your repo.

![image](https://user-images.githubusercontent.com/90503660/154623996-fb737749-45f0-4ebb-8329-f3d59d9ae653.png)

You could also verify and ensure that it didn't bring the remote branches during a bare clone

![image](https://user-images.githubusercontent.com/90503660/154625039-dc499776-2ff3-47e3-96e3-2a7b118c9fc5.png)

*NOTE:* Since this is a bare cloned repo, you wont be able to add anything to this repo. This is a bare repo meant only for migration. 
You can verify this with the git add commands,

![image](https://user-images.githubusercontent.com/90503660/154625160-f56b77c0-c081-4685-a758-92d27680022b.png)


### Add your target remote URL

`
git remote add azure https://kls13092021@dev.azure.com/kls13092021/DevOps%20Training/_git/Banking_Repo
`

![image](https://user-images.githubusercontent.com/90503660/154624129-95422da0-cd85-48fe-97e7-ece249488eb1.png)

### Push the locally cloned repository to Target(Azure Repos) using the “mirror” option

![image](https://user-images.githubusercontent.com/90503660/154624454-4d9df5cb-b7aa-4f1a-9de2-beff280848dc.png)

![image](https://user-images.githubusercontent.com/90503660/154624563-636d0a85-c61c-45d9-bfd5-d079f0282dc9.png)

### Verify the target repo in Azure Devops to see if the Source repo from GITHUB has been migrated successfully

![image](https://user-images.githubusercontent.com/90503660/154624687-201f7f34-37fd-4280-adb7-cff48f46b25a.png)

You could see all the files and history has been migrated successfully.

Repeat the same steps for all other repositories or write an automation script to perform the same for all repos.
