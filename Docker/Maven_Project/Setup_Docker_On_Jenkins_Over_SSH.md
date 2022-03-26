--- YYY ---
# To dockerize our Java Application, we need to setup Docker in our Jenkins Server.

1. Install Docker on Jenkins
2. Install Docker(Host) on the Target Machine(Deployment Server)
3. Create a "dockeradmin" user on the Docker Host & add it to the "docker" group
4. Install "Publish Over SSH" Plugin on Jenkins
5. Configure connectivity to Docker Host in Jenkins

## Install Docker on Jenkins Server & Deployment Server

Since we are using an Amazon EC2 server, go with the below URL for docker installation;
https://github.com/klsdevops/klsdevops/blob/main/Docker/1_Docker_Installation.md

## Create a "dockeradmin" user on the Docker Host(Deployment Server) & add it to the "docker" group

```
sudo useradd dockeradmin
```

```
sudo passwd dockeradmin
```

```
sudo usermod -aG docker dockeradmin
```

![image](https://user-images.githubusercontent.com/90503660/138026585-42128b1f-3775-4009-a265-e48d7fe3d533.png)

## Install "Publish Over SSH" Plugin on Jenkins

From the Jenkins UI -> Manage Jenkins -> Manage Plugins -> Available

Search for ssh and install "Publish Over SSH" plugin

![image](https://user-images.githubusercontent.com/90503660/138025525-341555b3-6902-4622-bf38-6317cdf21f04.png)

## Configure connectivity to Docker Host in Jenkins

From the Jenkins UI -> Manage Jenkins -> Configure System -> Publish Over SSH

![image](https://user-images.githubusercontent.com/90503660/138025039-088826c4-eaeb-4bed-a2ae-f54bf9904c45.png)

Under the section "Publish Over SSH", Click on "Add SSH Servers"

![image](https://user-images.githubusercontent.com/90503660/138025887-1c666db9-e1bd-4674-adf2-40c4abbeefbd.png)

Provide the below details
  * Name 
  * IP/Hostname
  * Username: dockeradmin
  
![image](https://user-images.githubusercontent.com/90503660/138026709-87a01c19-27a6-4c3d-909a-8a7acdc0b075.png)

Now go to the "Advanced" and provide further details
Choose password based authentication and provide the password and test the connection.

![image](https://user-images.githubusercontent.com/90503660/138026854-f17f064d-c804-449b-bd93-604d9db5b0f8.png)

**NOTE:** Since you are using the Amazon Linux machine, you will have to enable the password authentication on the ssh configuration on the Docker Host Machine before testing the connectivity. Otherwise you would get the below error while "test configuration"

![image](https://user-images.githubusercontent.com/90503660/138027035-86e6e4f5-a5c6-4356-8fab-0acb4f6b0ad6.png)

```
sudo vi /etc/ssh/sshd_config
```

Enable the PasswordAuthentication to "yes"

![image](https://user-images.githubusercontent.com/90503660/138027182-ce39c75f-ccc1-4aad-ad8b-52c5f6c6d7dc.png)

Restart sshd services

```
sudo service sshd restart
```

Now test the connectivity from Jenkins again and ensure its success,

![image](https://user-images.githubusercontent.com/90503660/138027429-227b335e-9a25-45d3-929e-6c62c639c3a7.png)

Save the settings.

# After setting up the docker & Jenkins connectivity, create a deployment pipeline on the Jenkins Console which copies the artifact to the Docker Host

![image](https://user-images.githubusercontent.com/90503660/138552275-5be0f83d-860a-4e48-9c52-a97d91123200.png)

Instead of creating a new job, we could copy from our existing job itself,

![image](https://user-images.githubusercontent.com/90503660/138552295-300bada5-8b85-4628-a5a9-de8baf403be6.png)

## Since we are not going to install to a VM directly, we could remove this from our existing pipeline

![image](https://user-images.githubusercontent.com/90503660/138552349-f81df8e9-f6f2-4e72-9f1d-27cece41dd0b.png)

## Select "Send Build artifact over SSH" from the "Post Build Actions" dropdown

![image](https://user-images.githubusercontent.com/90503660/138552390-ed1b93ba-67b0-4a96-b59a-c1ee6ec4e350.png)

Provide the details
  1. Select the Docker Host Machine as SSH Server
  2. Provide relative path of Source File to be transferred(eg; webapps/target/*.war) or if you dont know the exact location provide "**/*.war"
  3. Provide the remote directory location. We are giving it as "." as we need it to be available on the current directory(/home/dockeradmin)
 
![image](https://user-images.githubusercontent.com/90503660/138552827-9dd0a7d5-f50a-458c-b9f5-f27b55e63dc0.png)

## Verify on the Docker Host before executing the job

![image](https://user-images.githubusercontent.com/90503660/138552870-5b0d1b9a-8483-4279-9520-84eea3641dde.png)

## Build the job to test if the war file is getting copied to the Docker Host.

![image](https://user-images.githubusercontent.com/90503660/138552972-09e9a444-4d85-4e33-9bb7-45f61c4f5417.png)

## You could see the build is success & a file is transferred successfully.

## Verify the same on the docker host again

![image](https://user-images.githubusercontent.com/90503660/138553030-2a6c0d6d-de95-41bf-8160-c1fe80ebdfae.png)

## Now if you dont need the folder structure to be copied(webapp/target) and instead only the war file to be copied, we could configure/modify our job to remove prefix

![image](https://user-images.githubusercontent.com/90503660/138553113-2bfe0fa5-c629-4991-811b-c5d9ae386365.png)

## Now lets remove the current copied file from the Docker Host & execute the job one more time.

![image](https://user-images.githubusercontent.com/90503660/138553218-bb69ec17-fb8e-421e-b0e2-003fb3e59f2e.png)

## Now you could see its not copying the folder structure, but only the war file.

![image](https://user-images.githubusercontent.com/90503660/138553229-8492f5e0-e339-478b-be84-ca7d370a2157.png)
