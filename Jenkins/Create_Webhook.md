# Setting up a webhook for an automatic trigger of Jenkins Project
  
    1. Make sure the Jenkins GitHub plugin is installed in Jenkins
    2. In your Jenkins build job click the "GitHub hook trigger for GITScm polling" checkbox
    3. Create  a Jenkins API for the user with rights to run the build job
    4. In GitHub, create a webhook to trigger the Jenkins GitHub plugin
    5. Set the GitHub payload as "<JENKINS_URL>/github-webhook/"
    6. Set the Jenkins API Token as the webhook’s secret token
    7. Save the GitHub webhook configuration and watch Jenkins builds run without 403 no crumb errors
    
## Verify the Jenkins Plugin is installed in Jenkins

   Go to Jenkins -> Manage Jenkins -> Manage Plugins -> Installed Plugins 
   
   ![image](https://user-images.githubusercontent.com/90503660/135958947-eb4d93f7-7301-498a-be9d-f050ea0627b7.png)

## Create a Jenkins API Secret token

   Go to Jenkins -> Manage Jenkins -> Manage Users -> Select User (eg; root) -> Configure
   
   ![image](https://user-images.githubusercontent.com/90503660/135958776-cf95f7cc-a413-4ea7-92b2-2567cb385019.png)


## Select your repository -> Settings -> Webhooks -> Add Webhook

![image](https://user-images.githubusercontent.com/90503660/135957765-ad9957f3-6281-472b-a7fa-d6185bfd1c02.png)

## Provide the details for adding webhook

![image](https://user-images.githubusercontent.com/90503660/135957941-fbc96386-d11b-4627-b5a4-7bb3c9e8bf04.png)

## Watch URL Delivery run without 403 no crumb errors

![image](https://user-images.githubusercontent.com/90503660/135959113-d786aad4-51ed-40fc-a6a0-76abb5959da1.png)

![image](https://user-images.githubusercontent.com/90503660/135959210-86073b2e-1047-40ef-98eb-da3c943c9ed2.png)

## Enable "GitHub hook trigger for GITScm polling" checkbox in your Jenkins Job

![image](https://user-images.githubusercontent.com/90503660/135959299-7ca7e835-9fe4-409f-b884-050119604fdc.png)

## perform a manual build to see if the build is happening without any other issues

![image](https://user-images.githubusercontent.com/90503660/135959477-9d207d0e-e804-4020-a03c-fcfe47f9ab40.png)

## Update the Source Code & Push it to the Remote Repo

![image](https://user-images.githubusercontent.com/90503660/135959646-03e5a637-e96a-4d1d-a61f-f8a35b0faa62.png)

## Verify the Jenkins project

  ### You could see a build trigger has automatically started immediately the code is pushed to the remote repo.
  
  ![image](https://user-images.githubusercontent.com/90503660/135959727-a129ec59-e3d7-48e5-88f2-2698090e19cd.png)

## You can verify the latest update by starting the application & accessing the application web URL

  ### Start the application
  
  ![image](https://user-images.githubusercontent.com/90503660/135960037-0b70a4db-7104-44ab-af6a-652e458caeb5.png)

  ### Access the application on browser to see the updated code
  
  ![image](https://user-images.githubusercontent.com/90503660/135960093-a22276d5-7057-4d8f-be8e-ea96cae5d2d5.png)

