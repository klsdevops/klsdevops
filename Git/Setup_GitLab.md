# Setup a GitLab CE server
## System Requirements
### Software requirements

  Redis versions

  GitLab 13.0 and later requires Redis version 4.0 or higher.

### Hardware requirements
#### CPU 
CPU requirements are dependent on the number of users and expected workload.

The following is the recommended minimum CPU hardware guidance for a handful of example GitLab user base sizes.

4 cores is the recommended minimum number of cores and supports up to 500 users

8 cores supports up to 1000 users

#### Memory 
Memory requirements are dependent on the number of users and expected workload.

4GB RAM is the required minimum memory size and supports up to 500 users

8GB RAM supports up to 1000 users

# Installation Steps
### Install dependencies

There are a few dependencies that you must install before you install GitLab.

``
sudo yum install -y curl policycoreutils-python openssh-server postfix
``

![image](https://user-images.githubusercontent.com/90503660/152676442-8cfab153-f824-4f65-af7d-1ca7193013a2.png)


Enable Posix

``
sudo systemctl enable postfix && sudo systemctl start postfix
``

![image](https://user-images.githubusercontent.com/90503660/152676478-87c2d65e-9a76-4107-8aa6-4bfb785e21a9.png)

Install GitLab CE

* Change directory to /tmp:

``
cd /tmp
``

* Run the repository script from gitlab.com:

``
wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh
``

![image](https://user-images.githubusercontent.com/90503660/152676527-7ecf22c3-e66c-4117-b794-aae559c35341.png)

* Install the repository:

``
sudo bash script.rpm.sh
``

![image](https://user-images.githubusercontent.com/90503660/152676586-6660f48c-4cdb-4d86-b998-6c513fb269f2.png)


* install GitLab CE:

``
sudo yum install -y gitlab-ce
``

![image](https://user-images.githubusercontent.com/90503660/152676595-08707968-c794-431f-8009-785802172431.png)


#### Once the installation is completed, you will get the below screen

![image](https://user-images.githubusercontent.com/90503660/152676757-99d61e02-ebf2-4abf-97a4-db3c4f2a4ff6.png)


NOTE: You are recommended to change the password after installation.
https://docs.gitlab.com/ee/security/reset_user_password.html#reset-your-root-password


Thank you for installing GitLab!
GitLab should be available at http://ec2-18-218-121-105.us-east-2.compute.amazonaws.com


![image](https://user-images.githubusercontent.com/90503660/152676777-854060c1-e70e-40f6-9c5c-bb53966dbfd2.png)

### Read the initial root password

  ```
  cat /etc/gitlab/initial_root_password
  ```

![image](https://user-images.githubusercontent.com/90503660/152677149-6b958014-f0ed-4550-8d82-6bc4f5f9cfbe.png)


### Access the GITLAB UI using the URL: http://ec2-18-218-121-105.us-east-2.compute.amazonaws.com

![image](https://user-images.githubusercontent.com/90503660/152677120-a60f02cb-52cf-44b5-aaf4-0fa965fc9d5c.png)

#### Sign in with the "root" user & the initial password under "/etc/gitlab/initial_root_password"

![image](https://user-images.githubusercontent.com/90503660/152677371-acaa2727-bf67-4772-9a69-66db4a258de4.png)

#### Go to settings and change the password during the first login,

![image](https://user-images.githubusercontent.com/90503660/152677452-1775e696-a5a9-4bd7-8863-274d52b2e4cf.png)

NOTE: You could reset the access URL with your domain URL, setup the mail configuration etc from the configuration file "/etc/gitlab/gitlab.rb". 
Run "sudo gitlab-ctl reconfigure" command after saving the file.
