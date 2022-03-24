# Setup a Jenkins Controller using a docker container
### You could setup a Jenkins Controller with the official image "jenkins/jenkins"
### This is just an example to show a use case of docker containerization

Pull the Jenkins official image from the Docker Hub,

```
docker pull jenkins/jenkins
```

### Run a container with this image

```
docker run -d --name Jenkins_Controller -v jenkins_home:/var/jenkins_home -p 8080:8080 jenkins/jenkins
```

This will run Jenkins in detached mode with port forwarding and volume added. You can access logs with command 'docker logs CONTAINER_ID' in order to check first login token.


**-d** is for running in the detached mode

**--name** for providing a name for the container

**-v** for bind mount a volumes. This will automatically create a 'jenkins_home' docker volume on the host machine. Docker volumes retain their content even when the container is stopped, started, or deleted. You could see the volumes under "/var/lib/docker/volumes/" directory.

**-p** for port mapping 


![image](https://user-images.githubusercontent.com/90503660/159831740-dc4e1e7b-41b8-453e-89ae-3be753cd99f5.png)

### Now go to the browser and try to access the Jenkins Console with the "http://SERVER-IP:PORT" address
Here, in our example its "http://3.16.30.194:8080/"

![image](https://user-images.githubusercontent.com/90503660/159832025-22153898-5524-46eb-bc3f-59f31aa4855f.png)

You could see your jenkins controller machine is ready for setup.

You could check the container logs for getting the initial Admin password details

![image](https://user-images.githubusercontent.com/90503660/159832333-67d8655c-ff5f-425d-817a-334ef398444d.png)

Provide the password and continue with further steps,

![image](https://user-images.githubusercontent.com/90503660/159832433-146403d6-500e-447a-a8be-248f7516af43.png)

![image](https://user-images.githubusercontent.com/90503660/159832474-3dda438b-cb5f-403f-84dc-459755fdd3a5.png)

![image](https://user-images.githubusercontent.com/90503660/159832672-ebe4352d-0497-44ba-b506-bb7464b64981.png)

![image](https://user-images.githubusercontent.com/90503660/159832718-78ef28be-a7a4-4c5f-ace7-11436d3280e0.png)

![image](https://user-images.githubusercontent.com/90503660/159832741-6acbff8d-9fd6-48a8-b518-e68d15ca34fb.png)


## Your Jenkins Controller machine is Ready now.
