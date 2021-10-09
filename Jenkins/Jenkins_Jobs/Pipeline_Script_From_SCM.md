# Pre-requisites
1. Jenkins Server
2. Maven Installation
3. Maven Plugin Installation
4. Java Installation
5. Set JAVA_HOME, M2_HOME etc variables on the Jenkins Console
6. Tomcat server setup

# Refer the below document links for setting up Jenkins, Maven & Tomcat
  https://github.com/klsdevops/klsdevops/blob/main/Jenkins/Jenkins_Installation.MD
  https://github.com/klsdevops/klsdevops/blob/main/Jenkins/Maven_Installation.md
  https://github.com/klsdevops/klsdevops/blob/main/tomcat/Tomcat_Installation.md  

# Create a new item with "Pipeline" option

![image](https://user-images.githubusercontent.com/90503660/136666340-d4e348fa-baf3-4fc1-9b6c-68c06bbe0a70.png)

# Mention your GITHUB Project URL

![image](https://user-images.githubusercontent.com/90503660/136666404-e35f3663-fbea-4e99-a716-401602f55af3.png)

# Go to the "Pipeline" tab & Select the "Pipeline script from SCM" option from the dropdown
* Specify the SCM as "GIT"
* Provide the "Repository URL"
* If its a private repository, provide the credentials.(for our example we are using public repo & hence no credentials required)
* Specify the branch to build
* provide the script path. (your "Jenkinsfile" should be available under the root of your repository. Otherwise provide the relative path to the Jenkinsfile)

![image](https://user-images.githubusercontent.com/90503660/136666467-3a048517-8483-4ccc-82ac-257bfd1bfc0a.png)

![image](https://user-images.githubusercontent.com/90503660/136666667-5edf8eed-99c6-491e-83ab-e7c027feb41e.png)

# Ensure you have a "Jenkinsfile" in you repository, if not create a "Jenkinsfile" in your repository with the below code snippet

```
pipeline {
    agent any
    
    tools {
      maven 'M2_HOME'
      git 'Default'
      jdk 'JAVA_HOME'
    }
    
    environment {
      M2_HOME = "/opt/maven/apache-maven-3.8.2"
      M2 = "$M2_HOME/bin"
      JAVA_HOME = "/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.302.b08-0.amzn2.0.1.x86_64"
      PATH = "$M2_HOME:$M2:$JAVA_HOME/bin:$PATH"
    }
    
    triggers {
      pollSCM '* * * * *'
    }
    
    stages {     
        stage('Build') {
            steps {
                // Maven Build
                sh 'mvn clean install'
            }
        }
        
        stage('Deploy') {
            steps {
                // Deploy to tomcat server
                deploy adapters: [tomcat8(credentialsId: 'deployer', path: '', url: 'http://3.140.1.119:8090/')], contextPath: 'webapp', onFailure: false, war: '**/*.war'
            }
        }
    }
}
```

![image](https://user-images.githubusercontent.com/90503660/136666966-86a446ae-afe1-43d0-a30f-a3d122009ca3.png)

# Now trigger the pipeline & you could see the different stages running

![image](https://user-images.githubusercontent.com/90503660/136666919-ddf609a7-f585-47d5-adac-c8099b18f7e0.png)

# Verify the results by accessing the application URL

![image](https://user-images.githubusercontent.com/90503660/136667100-00c52af9-a90f-4f47-bbf2-f0b8013bd6dd.png)

