--- YYY ---

# Deploy on a docker container using Ansible through Jenkins

# Pre-Requisites
1. A jenkins Server
2. A Docker Host Machine
3. An Ansible Controller Machine
4. Connectivity between Ansible Controller & Jenkins
5. Connectivity between Ansible Controller & Docker Host
6. Connectivity between Ansible Controller & Docker Hub
7. A Dockerfile
8. A playbook for building the latest image with the Dockerfile
9. A playbook for Deploying the latest application on to the Docker Host machine
10. Create a Jenkins job for CICD (we can copy from our existing jobs)

## 1. A jenkins Server

To setup a Jenkins Server, Refer this https://github.com/klsdevops/klsdevops/blob/main/Jenkins/Jenkins_Installation.MD

## 2. A Docker Host Machine

To setup a Docker Host Machine, Refer this https://github.com/klsdevops/klsdevops/blob/main/Docker/Docker_Installation.md

Ensure the below are available on the Managed Host Machines(here, DockerHost)

* **please make sure that you are adding the "ansadmin" user to the Docker Host machine & also ensure its added as part of "docker" group.**

```
useradd ansadmin
passwd ansadmin
```

![image](https://user-images.githubusercontent.com/90503660/138592300-b883cac6-74ac-4c4e-b1d8-f5eed6ec35bf.png)

![image](https://user-images.githubusercontent.com/90503660/138592347-cee14b85-4004-4361-a625-fc9347e8a3d0.png)

* **Ensure "PasswordAuthentication" is enabled here as well as this is also a Amazon Linux server**

![image](https://user-images.githubusercontent.com/90503660/138592309-5c5e807d-ad7c-4750-aaab-faad1402f596.png)

* **Again, ensure the ansadmin user has given proper sudo privileges**

![image](https://user-images.githubusercontent.com/90503660/138592187-3c7f28e6-4dd5-43c4-86a9-10994f625f84.png)

**NOTE:** If sudo privileges are not given to the _ansadmin_ user you would see the below error while running the Jenkins Pipeline

![image](https://user-images.githubusercontent.com/90503660/138592395-496637d5-1be6-4551-a151-b8c008d08939.png)

## 3. An Ansible Controller Machine

To setup an Ansible Controller Machine, Refer this https://github.com/klsdevops/klsdevops/blob/main/Ansible/Ansible_Installation.md

## 4. Connectivity between Ansible Controller & Jenkins

Refer https://github.com/klsdevops/klsdevops/blob/main/Ansible/Integrate_Ansible_With_Jenkins.md

## 5. Connectivity between Ansible Controller & Docker Host

Ensure the ssh key has been copied from Ansible Controller to the Docker Host.

If not, Go to the Ansible Controller Machine and switch to "ansadmin" user & copy the rsa key to the DockerHost machine

```
sudo su - ansadmin
ssh-copy-id ansadmin@18.189.14.136
```

![image](https://user-images.githubusercontent.com/90503660/138592568-59fb6e3b-63b5-46be-9b8a-0bc6e24858cb.png)

Now you should be able to connect to the DockerHost machine from Ansible Controller machine without password

```
ssh ansadmin@18.189.14.136
```
![image](https://user-images.githubusercontent.com/90503660/138592584-bec91eba-1d8f-4c5a-ab7c-c2be217a721d.png)

## 6. Connectivity between Ansible Controller & Docker Hub

From the Ansible Controller run the "_docker login_" command by providing the **DockerHub** credentials of your account

```
docker login
```

![image](https://user-images.githubusercontent.com/90503660/138592641-7c9730f3-c415-40d6-8174-bbc7df6a2c3f.png)

**NOTE:** Ensure that you are executing the "docker login" command as root user. Otherwise you would encounter the below error while executing the Jenkins Pipeline

![image](https://user-images.githubusercontent.com/90503660/138592490-12b8cd91-f583-4cf2-b444-dfeed4c7ac50.png)

## 7. A Dockerfile 

Create a directory /opt/docker on the Ansible Controller Machine

```
sudo mkdir /opt/docker
sudo chown -R ansadmin:ansadmin /opt/docker
```

![image](https://user-images.githubusercontent.com/90503660/138588326-ca8e8c2f-df8f-4d37-835e-fcaa7f91938a.png)

Create a Dockerfile on the Ansible Controller under /opt/docker folder

```
# Pull tomcat latest image from dockerhub 
From tomcat:latest

# Maintainer
MAINTAINER klsdevops 

# copy war file on to container 
COPY ./webapp.war /usr/local/tomcat/webapps
```

![image](https://user-images.githubusercontent.com/90503660/138589423-58b3e2f1-8983-40ff-be5f-25b6e94507ae.png)

## 8. A playbook for building the latest image with the Dockerfile

```
# Option-1 : Creating docker image using command module 
---
- hosts: all
  become: true
  tasks:
  - name: building docker image
    command: docker build -t klsdevops/tomcat-app .
    args:
      chdir: /opt/docker
      
  - name: push image to Docker Hub
    command: docker push klsdevops/tomcat-app

  - name: Remove docker images from ansible controller
    command: docker rmi klsdevops/tomcat-app
    ignore_errors: yes

# option-2 : creating docker image using docker_image module 
#  tasks:
#  - name: building docker image
#    docker_image:
#      build:
#        path: /opt/docker
#      name: klsdevops/tomcat-app
#     tag: v1
#     source: build
```

![image](https://user-images.githubusercontent.com/90503660/138590816-fd13dd87-0fc3-41ec-98fd-aaa754816c0f.png)

## 9. A playbook for Deploying the latest application on to the Docker Host machine

```
---
- hosts: all
  become: true
  tasks:
  - name: stop if we have old docker container
    command: docker stop tomcat-app-container
    ignore_errors: yes

  - name: remove stopped docker container
    command: docker rm tomcat-app-container
    ignore_errors: yes

  - name: remove current docker image
    command: docker rmi klsdevops/tomcat-app
    ignore_errors: yes
#    register: result
#    failed_when:
#      - result.rc == 0
#      - '"docker" not in result.stdout'

  - name: pull docker image
    command: docker pull klsdevops/tomcat-app

  - name: creating docker image
    command: docker run -d --name tomcat-app-container -p 8080:8080 klsdevops/tomcat-app
```

![image](https://user-images.githubusercontent.com/90503660/138590457-2cb062d4-6760-41cc-981b-77e4e420e206.png)

## 10. Create a Jenkins job for CICD (we can copy from our existing jobs)

Create a new item from existing project

![image](https://user-images.githubusercontent.com/90503660/138588709-987a8e7c-1169-44ce-9e60-146bd79f6f47.png)

![image](https://user-images.githubusercontent.com/90503660/138588807-0ada09d5-fd39-4afe-b6b5-b96c7e0c3850.png)

From the existing pipeline **remove the Docker part** & Add Ansible execution part to the pipeline,

![image](https://user-images.githubusercontent.com/90503660/138592961-adbc6b1d-99d9-43f4-8129-d3382b7f39ce.png)

Replace it with the below Ansible content

![image](https://user-images.githubusercontent.com/90503660/138591008-f501b657-0de6-4540-8b60-4860b88cfa57.png)

**Note:** 
The first ansible playbook(_create-docker-image.yml_) is executing commands on the Ansible Controller(localhost) itself.
The Second ansbible playbook(_docker-deploy.yml_) is executing commands on the Managed Host(Dockerhost) machine.

## 11. Execute the pipeline and verify the results

The pipeline has been executed successfully and deployed the "war" file to the "Docker Host" deployment machine

![image](https://user-images.githubusercontent.com/90503660/138592818-5db9a14a-4443-4090-97ad-44bb440f3a31.png)

Verified the container & image from the Docker Host Machine

![image](https://user-images.githubusercontent.com/90503660/138592835-5e6fd262-1fc1-4a9d-b5d4-3e99ca42e474.png)

Verified the deployment by accessing the application from the browser as well,

![image](https://user-images.githubusercontent.com/90503660/138592886-5bc073f3-0d41-4c48-ae15-2fc04b3c1351.png)




