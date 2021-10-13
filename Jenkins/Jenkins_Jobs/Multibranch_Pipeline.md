# Multibranch Pipeline

The **Multibranch Pipeline** project type enables you to implement different Jenkinsfiles for different branches of the same project. In a Multibranch Pipeline project, Jenkins automatically discovers, manages and executes Pipelines for branches which contain a _Jenkinsfile_ in source control.

![image](https://user-images.githubusercontent.com/90503660/137160694-b3b3ca06-729c-44cf-a8da-a8c01198ebf7.png)

This eliminates the need for manual Pipeline creation and management.

# Create a "Develop" branch from the "Master" branch of the repository

![image](https://user-images.githubusercontent.com/90503660/136668389-344b4e93-1cb0-482e-a7ca-f02401996c2a.png)

# To create a multibranch pipeline, click on "new item" and select "Multibranch Pipeline" from the options & click OK

![image](https://user-images.githubusercontent.com/90503660/136667955-43911247-d322-4c04-b4d4-541b983c5ba8.png)

# Add a Branch Source (for example, Git) and enter the location of the repository.

![image](https://user-images.githubusercontent.com/90503660/136668017-0e68e41a-a824-4cca-9aae-2002052fcf33.png)

Save the Multibranch Pipeline project.

Upon Save, Jenkins automatically scans the designated repository and creates appropriate items for each branch in the repository which contains a _Jenkinsfile_.

![image](https://user-images.githubusercontent.com/90503660/136668375-e8da6a7c-954f-4098-84fb-cd277766aa62.png)

## You could see it has created two pipelines for the branches "Master" & "Develop"

## If you click on each pipeline, you could see the details of job executed 

![image](https://user-images.githubusercontent.com/90503660/136668487-3e33e239-9c9c-4201-95d9-70d56a3ec9ac.png)

## Ideally, your master code will have Production Environment details & Develop code will have Development environment details & the deployment happens to those respective servers.

# To enable autoscan for multibranch pipeline

* Install the plugin "Multibranch-scan-webhook-trigger"

![image](https://user-images.githubusercontent.com/90503660/136668874-dd2e5af7-6103-4ce8-963c-0f04aabc9dfb.png)

After installing this plugin, you will see a new area for "Scan Multibranch triggers"

![image](https://user-images.githubusercontent.com/90503660/136669066-4b78bc89-e401-4ded-8807-a34871bc6673.png)

## The selected line should be copied & used with the same token in the github settings while creating the webhook

# Add a webhook for the multiscan triggers

![image](https://user-images.githubusercontent.com/90503660/136669194-1b012cb0-7bb4-448d-974c-d43a8ab0107f.png)

![image](https://user-images.githubusercontent.com/90503660/136669300-ee1147a0-2b12-4327-a122-21d7f80a6e67.png)

![image](https://user-images.githubusercontent.com/90503660/136669304-ef0584b8-1b8c-43b9-9025-8706933577d7.png)

It will show you a tick mark.

# Make some updates in code & push the changes to remote

![image](https://user-images.githubusercontent.com/90503660/136669418-4f81ea02-1424-4533-ad87-26600af35a39.png)

You could see some automatic jobs has been triggered

![image](https://user-images.githubusercontent.com/90503660/136669445-4abf530b-4c34-4f36-8f40-bf89e830ba89.png)

![image](https://user-images.githubusercontent.com/90503660/136669467-879dcf75-e2ca-481d-8d34-4857d41e6200.png)

# Now if you want to see some automatic scans when we create a new branch, 

![image](https://user-images.githubusercontent.com/90503660/136669748-70354747-c413-4bcf-bc0b-6ac9e32e3883.png)

## Now you could see an automatic trigger has initiated & a new pipeline for UAT has been created

![image](https://user-images.githubusercontent.com/90503660/136669755-96b009ec-4fd6-4b5d-8b66-b3f855f8a56c.png)

# What happens if there's no Jenkinsfile in a branch ?

If there's no Jenkinsfile, it will not create any pipeline for that particular branch.

We can test it by removing Jenkins file from one branch & see,

For eg; we will remove Jenkinsfile from the newly created UAT branch,

![image](https://user-images.githubusercontent.com/90503660/136669966-f5aa02a2-e803-48de-baf8-52f479181789.png)

You could see Jenkinsfile has disappeared from Remote UAT branch

![image](https://user-images.githubusercontent.com/90503660/136669983-60512863-666a-4fb6-a535-5f898a9244e1.png)

When you check the multibranch pipeline, you could notice the "UAT" pipeline has been removed automatically

![image](https://user-images.githubusercontent.com/90503660/136670007-b4101b68-6e21-4155-9bfe-3b062712eea0.png)

# Usecases

## Now if the developer make changes & commit only to the Develop branch, then it will trigger only the Develop pipeline & do a deployment only to the development server.

* Change code on the Develop branch & commit

![image](https://user-images.githubusercontent.com/90503660/136670303-03bfd1b9-e85c-46a0-ba7e-d300cbc650d4.png)

* verify the pipeline to see the new automatic trigger on Develop Pipeline

![image](https://user-images.githubusercontent.com/90503660/136670326-dd896260-5717-4b81-ad69-e3468f52bbd3.png)

* Verify the changes on the application URL

![image](https://user-images.githubusercontent.com/90503660/136670338-a729c4a0-e0bf-4da6-8f10-c2f2af22d08a.png)

* You can verify the Production application URL (master) as well, it will be still having the old code update only

![image](https://user-images.githubusercontent.com/90503660/136670365-ddc03ff6-60b1-4260-bc7b-b9d8cb3e1b92.png)


