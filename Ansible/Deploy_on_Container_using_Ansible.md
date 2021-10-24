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

## 1. A jenkins Server

To setup a Jenkins Server, Refer this https://github.com/klsdevops/klsdevops/blob/main/Jenkins/Jenkins_Installation.MD

## 2. A Docker Host Machine

To setup a Docker Host Machine, Refer this https://github.com/klsdevops/klsdevops/blob/main/Docker/Docker_Installation.md

## 3. An Ansible Controller Machine

To setup an Ansible Controller Machine, Refer this https://github.com/klsdevops/klsdevops/blob/main/Ansible/Ansible_Installation.md

## 4. Connectivity between Ansible Controller & Jenkins

Refer https://github.com/klsdevops/klsdevops/blob/main/Ansible/Integrate_Ansible_With_Jenkins.md

## 5. Connectivity between Ansible Controller & Docker Host

## 6. Connectivity between Ansible Controller & Docker Hub

## 7. A Dockerfile 

Create a Dockerfile on the Ansible Controller under /opt/docker folder

```
# Pull tomcat latest image from dockerhub 
From tomcat:latest

# Maintainer
MAINTAINER "AR Shankar" 

# copy war file on to container 
COPY ./webapp.war /usr/local/tomcat/webapps
```

## 8. A playbook for building the latest image with the Dockerfile

```
# Option-1 : Createting docker image using command module 
---
- hosts: all
  become: true
  tasks:
  - name: building docker image
    command: docker build -t klsdevops/tomcat-app .
    args:
      chdir: /opt/docker

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
