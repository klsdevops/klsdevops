# To dockerize our Java Application, we need to setup Docker in our Jenkins Server.

1. Install Docker on Jenkins
2. Install Docker(Host) on the Target Machine(Deployment Server)
3. Create a "dockeradmin" user on the Docker Host & add it to the "docker" group
4. Install "Publish Over SSH" Plugin on Jenkins
5. Configure connectivity to Docker Host in Jenkins

## Install Docker on Jenkins Server/Deployment Server

Since we are using an Amazon EC2 server, go with the below URL for docker installation;
https://github.com/klsdevops/klsdevops/blob/main/Docker/Docker_Installation.md

## Create a "dockeradmin" user on the Docker Host & add it to the "docker" group

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
