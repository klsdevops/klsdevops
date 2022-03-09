# Pre-requisites
1. Jenkins Server
2. Maven Installation
3. Maven Plugin Installation
4. Java Installation
5. Set JAVA_HOME, M2_HOME etc variables on the Jenkins Console
6. Tomcat Server setup

# Refer the below document links for setting up Jenkins, Maven & Tomcat
  https://github.com/klsdevops/klsdevops/blob/main/Jenkins/1_Jenkins_Installation.MD
  https://github.com/klsdevops/klsdevops/blob/main/Jenkins/2_Maven_Installation.md
  https://github.com/klsdevops/klsdevops/blob/main/tomcat/5_Tomcat_Installation.md
  

# Create a new item with "Pipeline" option

![image](https://user-images.githubusercontent.com/90503660/136646868-b318d12a-5780-42c4-9551-977076da143b.png)

# Go to the "Pipeline" tab and write a declarative script for building the application using Maven

![image](https://user-images.githubusercontent.com/90503660/136647172-6e0febce-800d-40f4-9f36-3e22111f63ad.png)

**NOTE:** You can always use the "Pipeline Syntax" option for writing the code snippet
http://3.22.222.129:8080/job/maven-scm-pipeline/pipeline-syntax/

## You can copy & paste the below code snippet

```
pipeline {
    agent any
    tools {
      maven 'M2_HOME'
      git 'Default'
      jdk 'JAVA_HOME'
    }
    environment {
      M2_HOME = "/opt/maven/apache-maven-3.8.4"
      M2 = "$M2_HOME/bin"
      JAVA_HOME = "/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-1.amzn2.0.2.x86_64"
      PATH = "$M2_HOME:$M2:$JAVA_HOME/bin:$PATH"
    }
    stages {
        stage('Checkout') {
            steps {
                // Get some code from a GitHub repository
                git changelog: false, url: 'https://github.com/klsdevops/sample-maven-project.git'
            }
        }
        
        stage('Build') {
            steps {
                // Maven Build
                sh 'mvn clean install'
            }
        }
    }
}
```

# Run your pipeline 

![image](https://user-images.githubusercontent.com/90503660/136647205-d2730668-add5-492e-9e82-53fca46aec09.png)

## You could see different stages running with a stage view

![image](https://user-images.githubusercontent.com/90503660/136647220-5f5ce9b8-afcc-42d4-bd81-602eca8cd017.png)

## Click on the "logs" to see the tasks in details

![image](https://user-images.githubusercontent.com/90503660/136647271-47707066-de7f-4efe-921a-5d62ce26feb3.png)

## You can view the complete logs from the console output

![image](https://user-images.githubusercontent.com/90503660/136647297-300aeff4-5638-4eb1-8b08-b2a1afb6033f.png)

## If you want to enable PollSCM Triggers, you can add the below code snippet

```
    triggers {
      pollSCM '* * * * *'
    }
```

![image](https://user-images.githubusercontent.com/90503660/136647842-791f545f-e038-4329-8cb9-55b195727c39.png)

## Now we will add the code snippet for the deployment part as well

```
deploy adapters: [tomcat8(credentialsId: 'deployer', path: '', url: 'http://3.140.1.119:8090/')], contextPath: 'webapp', onFailure: false, war: '**/*.war'
```

![image](https://user-images.githubusercontent.com/90503660/136665594-86ca5844-49c6-4bf8-bce9-03f8aac96be8.png)

## Once you run the pipeline, you could see a new view for the "Deploy" running on the pipeline

![image](https://user-images.githubusercontent.com/90503660/136665643-279a9026-ff14-49db-804c-81774eb5fc77.png)

## Verify the output by checking the application URL

![image](https://user-images.githubusercontent.com/90503660/136666999-2e4d49fc-43fb-4a7f-b24d-8531ca1771dc.png)

