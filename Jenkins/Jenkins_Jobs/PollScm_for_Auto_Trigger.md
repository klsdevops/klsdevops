# To trigger a build automatically when a code update happens in github repository, using the PollSCM option of Jenkins build triggers

## 1. Edit the pipeline and enable PollSCM Options and Save it.
   
   ### Go to the Deployment pipeline(Deploy_on_Tomcat_Server) and click on the "Configure" button,
   
   ![image](https://user-images.githubusercontent.com/90503660/135784277-3391e86a-6f43-4130-9a66-8496ae219cde.png)

   ### In the "Build Triggers" tab, click on the "Poll SCM" Checkbox and set the cron entry for what time you need the trigger to happen
   
   ![image](https://user-images.githubusercontent.com/90503660/135784387-6ef46531-a4f3-4a3e-931f-d621f6b15e9c.png)

   ### In our Demo, we are setting it as for every minutes so the it will check for an update every minute and trigger the pipeline accordingly after a code update.
   
## 2. Edit the code and push it to Remote Repo (GITHUB)

   ![image](https://user-images.githubusercontent.com/90503660/135784670-f346f13d-8d95-48c3-a508-52a8cdc9ced8.png)

   ### Commit and Push the code
   
   ![image](https://user-images.githubusercontent.com/90503660/135784722-ea947248-ab63-4c2f-8aee-0df4c8af6d01.png)

   ### Verify if the code has updated in the Remote Repo,
   
   ![image](https://user-images.githubusercontent.com/90503660/135784785-d5577395-4f93-4525-878a-f021e6b2bf16.png)

## 3. Verify the pipeline to see if a new trigger has happened automatically,
   
   ![image](https://user-images.githubusercontent.com/90503660/135784200-3731f9aa-f665-486d-a8ee-0b0cbdf2719a.png)

   ### You could see a new build has automatically triggerd. (Initially it shows as pending and then it progress to running & then successfully done).
   
## 4. Verify the application deployed.
  
   ![image](https://user-images.githubusercontent.com/90503660/135784963-f0812b3d-0149-40a3-95d1-df500e368827.png)

   ### You could see the latest code changes is reflecting in the application now.
   
   
