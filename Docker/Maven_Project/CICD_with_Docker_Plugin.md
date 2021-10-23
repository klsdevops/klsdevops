# Alternate method to create a CICD pipeline with dockerizing the application

1. Install Docker on the Jenkins Server
2. Install "Cloudbees Docker Build and Publish" plugin
3. Create a Dockerfile & keep it in your GITHUB Repository under root location
4. Create a Repository in the Docker Hub for this application
5. Create the Jenkins Credentials for the Docker Hub access
6. Ensure _jenkins_ user is part of the _docker_ group on the Jenkins Server
7. Create a new pipeline
8. Execute the pipeline & see how the Build and Deployment is happening

## 1. Install Docker on the Jenkins Server

Refer https://github.com/klsdevops/klsdevops/blob/main/Docker/Docker_Installation.md

## 2. Install "Cloudbees Docker Build and Publish" plugin

![image](https://user-images.githubusercontent.com/90503660/138508917-8dff997b-6201-4b7f-bca2-6a8845a22abf.png)

## 3. Create a Dockerfile & keep it in your GITHUB Repository under root location

With respect to the application you have developed, write your Dockerfile & push it to your GITHUB project repository

```
# A Dockerfile based on centos OS for running tomcat application
FROM centos:7

MAINTAINER klsdevops

WORKDIR /opt
RUN yum -y install wget java-1.8* && \
    wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.72/bin/apache-tomcat-8.5.72.tar.gz --no-check-certificate && \
    tar xvfz apache*.tar.gz && \
    rm *.tar.gz && \
    mv apache-tomcat-* tomcat && \
    ln -s /opt/tomcat/bin/catalina.sh /usr/local/bin/catalina.sh

ENV CATALINA_HOME /opt/tomcat/

COPY webapp/target/webapp.war /opt/tomcat/webapps/

EXPOSE 8080

CMD ["catalina.sh", "run"]
```

![image](https://user-images.githubusercontent.com/90503660/138560061-760029c4-5da1-43c8-bb52-4fd812b658b8.png)

## 4. Create a Repository in the Docker Hub for this application

Go to the https://hub.docker.com/ website and Click on "Create Repository" button

![image](https://user-images.githubusercontent.com/90503660/138559860-f0e03160-c7bb-40f8-a0a0-180a87b61185.png)

Provide the repository details & press the "Create" button

![image](https://user-images.githubusercontent.com/90503660/138559936-e4be990e-e431-4671-85c5-616bfc89bc0b.png)

You should be able to see the list of repositories in your DockerHub account

![image](https://user-images.githubusercontent.com/90503660/138559973-122f14dc-0b21-4ae5-85c8-a22c594f2237.png)

## 5. Create the Jenkins Credentials for the Docker Hub access

Go to Jenkins Dashboard -> Manage Jenkins -> Manage Credentials -> Add Credentials(Global)

![image](https://user-images.githubusercontent.com/90503660/138560354-d2e78f17-e6d9-4593-9ea6-17c09e0c86e0.png)

## 6. Ensure _jenkins_ user is part of the _docker_ group on the Jenkins Server

Before running docker commands from jenkins "Execute Shell", make sure that the docker group is added to the jenkins user

![image](https://user-images.githubusercontent.com/90503660/138393576-f4902bcf-41a2-4971-980e-dd256d8db98a.png)

and restart the jenkins services

![image](https://user-images.githubusercontent.com/90503660/138393798-1a59b626-d0e8-4544-abd6-55b1cc91d3c4.png)

otherwise you would see the below error;

![image](https://user-images.githubusercontent.com/90503660/138393644-dec156df-2c46-42ef-8b2e-38f2119652b7.png)

## 7. Create a new Maven Pipeline (copy from existing one)

![image](https://user-images.githubusercontent.com/90503660/138558739-f05b80fd-aba7-4055-81cc-8a045dff2919.png)

![image](https://user-images.githubusercontent.com/90503660/138558753-92baccfe-a2e7-479f-85a0-4947e0f962e9.png)

### You could test if the docker commands are working as expected through "Execute Shell" method 

![image](https://user-images.githubusercontent.com/90503660/138560159-513d9635-0c5c-4495-987d-d668586ea0b6.png)

Once you execute the pipeline, you could see the Maven Build is success & it has created the docker image of our application

![image](https://user-images.githubusercontent.com/90503660/138559519-037b92eb-3466-4edd-90dd-4a79c73430e2.png)

You could check on the Jenkins Server & see a new image has been created there

![image](https://user-images.githubusercontent.com/90503660/138559590-dcca99e7-01ab-4cb3-b609-90c24f3e1d6b.png)

**_So now, you have verified that your pipeline is picking up the Dockerfile from the GIT repo & able to execute docker commands in the Jenkins Server & its successfully creating a Docker Image._**

## Now, instead of using the "Execute Shell" method & writing docker commands in it, you could use docker plugins(Cloudbees Docker Build and Publish)

## Modify the pipeline & use the "Docker build & Publish" option from the "Add post Build Step"

![image](https://user-images.githubusercontent.com/90503660/138509316-0c198500-cd83-4a57-9ca7-07b82040dc62.png)

![image](https://user-images.githubusercontent.com/90503660/138510761-f27b4c8a-161e-4b70-9af9-bc58aff70052.png)

**NOTE:** 
You could leave the **_Docker Host URI_** as blank as of now.
You could keep the **_Docker Registry URL_** as empty as it takes dockerhub by default.

## 8. Execute the pipeline & see how the Build and Deployment is happening

![image](https://user-images.githubusercontent.com/90503660/138560457-9da53a3d-a8c2-4291-bd9d-95f68518e29d.png)

So this is creating a docker image of our application & pushing it to the Docker Registry(DockerHub).

You could verify it on the Docker Hub repository

![image](https://user-images.githubusercontent.com/90503660/138560825-62df12da-78f5-4575-9b1c-0e585a5f2cdc.png)


