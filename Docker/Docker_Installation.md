# Docker CE Installation on Amazon Linux:
1. Update the installed packages and package cache on your instance

```
sudo yum update -y
```

![image](https://user-images.githubusercontent.com/90503660/137362366-51519a3a-3f16-4ce6-82eb-23e97cce74b1.png)


2. Install the most recent Docker Engine package.

  **For Amazon Linux 2:**
```
sudo amazon-linux-extras install docker
```

  **For Amazon Linux:**
```
sudo yum install docker
```

![image](https://user-images.githubusercontent.com/90503660/137362514-4ea52fd6-ff81-4aa7-98f4-98d027eedffc.png)


3. Start the Docker service

```
sudo service docker start
```

![image](https://user-images.githubusercontent.com/90503660/137362634-405d0dce-db8d-42a1-bca3-90e6b4e9cc55.png)


4. Make docker auto-start

```
sudo chkconfig docker on
```

![image](https://user-images.githubusercontent.com/90503660/137362709-de5b6012-073b-4f4a-91d5-8c1d77efa233.png)


5. Add the ec2-user to the docker group so you can execute Docker commands without using sudo.

```
sudo usermod -a -G docker ec2-user
```

![image](https://user-images.githubusercontent.com/90503660/137363002-e12772ac-5f16-4762-9882-cc215a451041.png)


6. Log out and log back in again to pick up the new docker group permissions.

7. Verify that the ec2-user can run Docker commands without sudo.

```
docker info
```

![image](https://user-images.githubusercontent.com/90503660/137363076-4a29355a-a349-47ae-b175-55eb966cc042.png)


**NOTE:** Sometimes you may need to reboot your instance to provide permissions for the ec2-user to access the Docker daemon. Try rebooting your instance if you see the following error:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

![image](https://user-images.githubusercontent.com/90503660/137363185-a8cae334-b08a-49b3-9122-adac0f48cb22.png)


# Easy method using the script for Linux Distros

The purpose of the install script is for a convenience for quickly installing the latest Docker-CE releases on the supported linux distros. 
It is not recommended to depend on this script for deployment to production systems

```
curl -fsSL https://get.docker.com/ | sh
```

![image](https://user-images.githubusercontent.com/90503660/137366336-389c6c0a-bc06-4dab-80e6-35febb04f366.png)

Start the docker services & Verify the Docker Version installed

![image](https://user-images.githubusercontent.com/90503660/137366491-4fef7d9f-ac65-40ac-8c0a-b5d9e1d23e1d.png)


