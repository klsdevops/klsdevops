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

Refer https://github.com/klsdevops/klsdevops/blob/main/Docker/1_Docker_Installation.md

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

Provide the DockerHub credentials here

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

# Now we need to perform the Application Deployment.

So far what we have done is the below as part of Build Pipeline (CI)
1. Build the application(Maven Build)
2. Package it as a docker image
3. Pushed the application image to the Docker Registry.

Now we need to deploy this application to a target deployment server. Hence we will have to do few more activities
1. Launch a Target Machine (EC2 instance)
2. Install Docker on it
3. Setup the docker daemon to 
4. Update the Jenkins Pipeline with the deployment steps
5. Execute the Pipeline & verify the Results

## 1. Launch a Deployment Server(Docker Host) target machine

![image](https://user-images.githubusercontent.com/90503660/138561155-42ac7e75-4f53-47e4-a1b0-6121ba80dd65.png)

## 2. Install Docker on to it

Refer https://github.com/klsdevops/klsdevops/blob/main/Docker/1_Docker_Installation.md

## 3. Update the Jenkins Pipeline with the deployment steps

Add another post build action to execute the docker deployment commands

```
#docker -H tcp://13.58.253.153:2375 stop tomcat-prod-app
#docker -H tcp://13.58.253.153:2375 rm tomcat-prod-app
docker -H tcp://13.58.253.153:2375 run -it -d --name tomcat-prod-app -p 8080:8080 klsdevops/tomcat-app:$BUILD_NUMBER
```

![image](https://user-images.githubusercontent.com/90503660/138563439-e813a041-f5ae-4b02-9b9f-b3fc29c7b50a.png)

**NOTE:**
13.58.253.153 is the Docker Host IP Address
2375 is the unencrypted docker socket, remote root passwordless access to the host
**Also ensure to enable the port 2375 in your AWS Security Group inbound rules**

Here after executing the pipeline, you would see that its failing because it can not connect to the docker daemon on the Docker Host machine

![image](https://user-images.githubusercontent.com/90503660/138562106-1ad6d618-ac81-476d-b518-479a284ce54a.png)

To rectify this issue, you should update some docker settings in the Docker Host Machine.

Edit the "/usr/lib/systemd/system/docker.service" file & add " -H tcp://0.0.0.0:2375 " to the "ExecStart=/usr/bin/dockerd -H fd:// " line

![image](https://user-images.githubusercontent.com/90503660/138562478-6f066d2f-ef1f-49ea-8d91-3831c3a80594.png)

The below is the complete process for updating the settings

![image](https://user-images.githubusercontent.com/90503660/138563017-51c6d38a-a5d7-4acd-a9ba-e91529cb065e.png)

```
netstat -lntp | grep dockerd
systemctl status docker.service
vi /usr/lib/systemd/system/docker.service
    # amend "ExecStart" line with -H tcp://0.0.0.0:2375
systemctl daemon-reload
systemctl restart docker.service
netstat -lntp | grep dockerd
```
## Now build the pipeline again and see the results

![image](https://user-images.githubusercontent.com/90503660/138563489-c493e382-199c-426e-9cc5-450d5a55abce.png)

You could see the build is successful at the Jenkins end.

You could verify the same on the Docker Host Machine as well,

![image](https://user-images.githubusercontent.com/90503660/138563513-e1db647b-905b-4b3f-a267-bb593b8cf3a9.png)

A container "tomcat-prod-app" is running on this machine.

# Verify the application from the browser

![image](https://user-images.githubusercontent.com/90503660/138563539-e2642f07-2b70-4040-a096-13a23d0387da.png)

