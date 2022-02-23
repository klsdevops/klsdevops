# Create a First Maven Jenkins job to build hello-world project 
# *Jenkins Job name:* `My_First_Maven_Build`

We know how to work with Git and Jenkins independently. What if you want to collaborate these two?  Follow the below steps;

## Pre-requisites

1. Jenkins server 
2. Maven
3. Git

## Fork the https://github.com/klsdevops/sample-maven-project.git

## Steps to create "My_First_Maven_Build" Jenkin job
1. **Login to Jenkins console**
2. **Click on "New Item" and Provide the Item Name & Select "Maven Project" and click "OK"**
    
    ![image](https://user-images.githubusercontent.com/90503660/135743522-6cb00440-393c-4e53-850e-d6ba3f3bdef4.png)

3. **Create *Jenkins job*, Fill the following details,**
   - *Source Code Management:*
      - Repository: `https://github.com/klsdevops/sample-maven-project.git`
      - Branches to build : `*/master`  
   - *Build:*
     - Root POM:`pom.xml`
     - Goals and options: `clean install package`

    **The Jenkins Screens**
    
    ![image](https://user-images.githubusercontent.com/90503660/135743654-8658b060-e6c9-45bf-9547-4780318ca3ea.png)

    ![image](https://user-images.githubusercontent.com/90503660/135743679-a24ae68f-f933-44a3-af56-791724c484da.png)
  
    ![image](https://user-images.githubusercontent.com/90503660/135743711-784e3eff-2fdb-4f76-abe6-cc57cdcd4ed2.png)

    ![image](https://user-images.githubusercontent.com/90503660/135743756-b384e47c-b7be-47f0-a456-82fac6d45bdc.png)

4. **Trigger a build job now,**
    
    ![image](https://user-images.githubusercontent.com/90503660/135743823-85e83446-c6cc-45c3-aed9-145fd118a5e9.png)

    **Now you could see a job has started**
    
    ![image](https://user-images.githubusercontent.com/90503660/135743844-f7af4db8-a8cc-4015-adb4-cdf1ded7941c.png)

    **Once the job is completed, it will show the status** 
    
    ![image](https://user-images.githubusercontent.com/90503660/135743865-366653d6-eeb3-42f5-be78-bddc0ee6d130.png)

    **Click on it to see details**
    
    ![image](https://user-images.githubusercontent.com/90503660/135743881-09e9d44c-818c-4723-b9c0-656e864a53b7.png)

    **Click on the "Console Output" to see the build log**
    
    ![image](https://user-images.githubusercontent.com/90503660/135743923-20daee5a-793e-4fec-b673-11a1d2c0759a.png)

    **You could go through the Log to see what has happened during the build & at the end you can see the build results,**
    
    ![image](https://user-images.githubusercontent.com/90503660/135743947-0529db4b-09a5-452b-bebe-3f25c6fc1bb5.png)

    **Click on the "Workspace", you will see jenkins has copied the entire content of your source code from GIT to Jenkins Agent's Workspace location**
    
    ![image](https://user-images.githubusercontent.com/90503660/135744042-06d05c60-6170-4296-806f-eda0e931efc3.png)

    **Under the webapps/target folder of workspace, you can see an artifact has been created**
    
    ![image](https://user-images.githubusercontent.com/90503660/135744093-20f97719-3820-4fc2-9308-524ceca2adce.png)

    **You can see the same results on your Jenkins Agent Machine using CLI,**
    
    ![image](https://user-images.githubusercontent.com/90503660/135744170-230819ad-da57-4863-8e4e-d252f1256855.png)

 ### This how you will build a maven based java application using Jenkins.
