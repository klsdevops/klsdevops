# Deploy on a Tomcat server
# *Jenkins Job name:* `Deploy_on_Tomcat_Server`

### Pre-requisites

1. Jenkins server 
2. Tomcat Server 

### Adding Deployment steps

1. Install 'deploy to container' plugin. This plugin needs to deploy on tomcat server. 

  - Install 'deploy to container' plugin without restart  
    - `Manage Jenkins` > `Jenkins Plugins` > `available` > `deploy to container`

    ![image](https://user-images.githubusercontent.com/90503660/135749649-3eb0d841-8674-4f3a-bc84-f2aeb1ade3e0.png)

 
2. Jenkins should need access to the tomcat server to deploy build artifacts. setup credentials to enable this process. use credentials option on Jenkins home page.

- setup credentials
  - `credentials` > `jenkins` > `Global credentials` > `add credentials`
    - Username	: `deployer`
    - Password : `deployer`
    - id      :  `deployer`
    - Description: `user to deploy on tomcat vm`
    
    ![image](https://user-images.githubusercontent.com/90503660/135749917-9a5661cc-52a3-4cf0-b1a0-42f29949f18b.png)

### Steps to create "Deploy_on_Tomcat_Server" Jenkin job
 #### From Jenkins home page select "New Item"
   - Enter an item name: `Deploy_on_Tomcat_Server`
     - Copy from: `My_First_Maven_Build`
     
   - *Source Code Management:*
      - Repository: `https://github.com/klsdevops/sample-maven-project.git`
      - Branches to build : `*/master`  
   - *Poll SCM* :      - `* * * *`

   - *Build:*
     - Root POM:`pom.xml`
     - Goals and options: `clean install package`

 - *Post-build Actions*
   - Deploy war/ear to container
      - WAR/EAR files : `**/*.war`
      - Containers : `Tomcat 8.x`
         - Credentials: `deployer` (user created on above)
         - Tomcat URL : `http://<PUBLIC_IP>:8080`
    
    ![image](https://user-images.githubusercontent.com/90503660/135749995-b529b0a5-e2ed-4b24-aa64-e1ddd92a0748.png)

    ![image](https://user-images.githubusercontent.com/90503660/135750005-94a6b9f8-8778-488a-87e8-0fa115c21d03.png)

Save and run the job now.

    ![image](https://user-images.githubusercontent.com/90503660/135750033-e682ba4c-6f1a-497a-a621-5070f367baab.png)

Once the build is success, go to the Browser URL and check the application deployed under the "webapps" folder.

![image](https://user-images.githubusercontent.com/90503660/135750077-db4e08de-13e3-4cca-817e-a61affbc77ad.png)


