# Install ansible on Amazon Linux EC2 instance

Ansible is an open-source automation platform. Ansible can help you with configuration management, application deployment and task automation.

## Pre-requisites
* An AWS EC2 instance (Control node)
* Python

## Installation steps:
On Amazon EC2 instance

1. Install python and python-pip

```
yum install python
yum install python-pip
```

On the Amazon Linux machine, python is installed by default

![image](https://user-images.githubusercontent.com/90503660/138581347-79b4adb9-64d1-49a6-879a-3b90d9d39d8a.png)

Now, install python-pip

![image](https://user-images.githubusercontent.com/90503660/138581362-921ed61b-53fd-43f8-8047-6ba5446746d8.png)

2. Install Ansible using python pip

```
pip install ansible
ansible --version
```

![image](https://user-images.githubusercontent.com/90503660/138581444-8988c8f1-5d02-4890-9aa1-d8a068d3fea5.png)

3. For newer versions of Ansible, it doesn't have the default ansible configuration folder. So please create a directory /etc/ansible and create an inventory file called "hosts". Add localhost and Managed Hosts(eg; Docker Host machine) IP addresses to it.

```
mkdir /etc/ansible
vi /etc/ansible/hosts
  # Add target machine's IPs to it
  18.189.14.136
  localhost
```

![image](https://user-images.githubusercontent.com/90503660/138581514-95af2390-5322-4c06-be5e-c03c18f6c46f.png)

4. Create a user called ansadmin (on Controller machine). You will have to create the same user on the target(Managed Hosts) machines as well.

```
useradd ansadmin
passwd ansadmin
```

![image](https://user-images.githubusercontent.com/90503660/138581577-deb0cda3-e280-4afd-a646-a1e624a8fa44.png)

5. Grant sudo access to **_ansadmin_** user

```
visudo
  ## Add this line at the end of the /etc/sudoers file "ansadmin ALL=(ALL) NOPASSWD: ALL"
```

![image](https://user-images.githubusercontent.com/90503660/138581740-508b5412-b96f-463e-8ee2-38a553804759.png)

6. Enable "_PasswordAuthentication_" in the "_/etc/ssh/sshd_config_" file and reload the sshd services

![image](https://user-images.githubusercontent.com/90503660/138581901-1f702597-9176-4192-a1d2-364b8f976ca2.png)

![image](https://user-images.githubusercontent.com/90503660/138581950-c08dbef4-b36f-4e09-a249-e07236c03151.png)

7. Log in as a ansadmin user on Ansible Controller machine and generate ssh key

```
sudo su - ansadmin
ssh-keygen
```

![image](https://user-images.githubusercontent.com/90503660/138581971-5f30a32f-3edd-43be-8c5d-eab7a6f4dbc9.png)

You could see the rsa keys are generated under ".ssh" directory

![image](https://user-images.githubusercontent.com/90503660/138581985-eda1d587-02f7-4c16-9fa5-776e53a806cb.png)

8. This key should be copied to all the target machines (Managed Hosts)

```
ssh-copy-id ansadmin@<target-server>
```

9. Since in our example/demo we are going to do a docker deployment through Jenkins machine, we need to install Docker on the Ansible Controller & then copy the rsa keys to the Docker Host machine.

```
yum install -y docker
docker --version
systemctl start docker
chkconfig docker on
systemctl status docker
```

![image](https://user-images.githubusercontent.com/90503660/138582132-a3187f68-602c-4934-8aca-fa10b351da40.png)

Add "_ansadmin_" user to the "_docker_" group,

```
usermod -aG docker ansadmin
```

![image](https://user-images.githubusercontent.com/90503660/138582166-b7100aeb-b2b6-46a3-acdd-5a7a17f55bb9.png)

10. Login to the Docker Host machine & create "_ansadmin_" user there as well

```
useradd ansadmin
passwd ansadmin
```

![image](https://user-images.githubusercontent.com/90503660/138582308-eb77a936-c34f-4e50-9464-b3fac7d1b721.png)

Ensure "_PasswordAuthentication_" is enabled here as well as this is also a Amazon Linux server

![image](https://user-images.githubusercontent.com/90503660/138582328-ba30dd21-b349-467b-b9d6-a392d5f492a3.png)

Also add "_ansadmin_" user to the "_docker_" group

![image](https://user-images.githubusercontent.com/90503660/138590185-d5403c2a-49f4-4be4-b0cf-51339cc905e5.png)

11. Go to the **Ansible Controller** Machine and switch to "_ansadmin_" user & copy the rsa key to the **DockerHost** machine 

```
sudo su - ansadmin
ssh-copy-id ansadmin@18.189.14.136
```

![image](https://user-images.githubusercontent.com/90503660/138582491-b2cc94d6-48a3-49af-b0e1-e2bee69836fd.png)

Now you should be able to connect to the DockerHost machine from Ansible Controller machine without password

```
ssh ansadmin@18.189.14.136
```
![image](https://user-images.githubusercontent.com/90503660/138582532-7f8d187a-851b-4dbc-a297-cab656ffe951.png)

12. Go to Ansible Controller Machine & add the Docker Host's IP to the inventory file

![image](https://user-images.githubusercontent.com/90503660/138582708-7c5c355b-bb6a-4fdf-ba43-f3d1da0cece1.png)

13. Switch to "_ansadmin_" user & try an Ansible Ping test

![image](https://user-images.githubusercontent.com/90503660/138582743-9ce800ac-b81f-4a6b-9f20-e50b24d921c6.png)

You could see the Ping test to the DockerHost machine is successful. But the localhost is failed as we didn't copy the ssh key to localhost.

**NOTE:**
We will copy the ssh key to localhost and do a ping test again.

![image](https://user-images.githubusercontent.com/90503660/138582798-48ee91f6-9d78-4e2f-8fb0-077780f7a35a.png)

Now we ensured our Ansible Controller Machine is able to communicate with the Managed Host Machine.
