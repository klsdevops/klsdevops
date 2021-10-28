# Here are some basic commands

Docker Commands:

**1. run - Start a container**

```
	 docker run nginx
```

**2. ps - list containers**

```
	docker ps
```	

To see all containers

```
	docker ps -a
```

**3. stop - STOP a container**

```
	docker stop <container-name>
```

**4. rm - Remove a container**

```
	docker rm <container-name>
```

**5. images - List images**

```
	docker images
```

**6. rmi - Remove images**

```
	docker rmi nginx
```

**7. pull - download an image**

```
	docker pull nginx
```

**8. exec - Execute a command**

```
	docker exec <container-name> <command>
```

**9. run - attach and detach**

Attached mode:

```
	docker run nginx
```
Detached mode:

```
	docker run -d nginx
```

This will run the docker container in the background.
If you want to attach to the container on a later stage, you could use the below command,

```
	docker attach <container-name>
```

**10. run - tag**
```
	docker run redis:4.0
```

If not specifying a tag explicitly as above, docker will take the latest tag by default.
	
**11. run - stdin**

```
	docker run -it nginx
```
-i = interactive mode
-t = psuedo terminal
	
**12. run - port mapping**

```
	docker run -p 80:5000 nginx
```

-p = port mapping
left side of column(80) is "host port" and right side of column(5000) is "container port"
So all traffic on port 80 on docker host will get routed to port 5000 inside the docker container.
	
eg; if you want to run tomcat on a container, it can use the default port 8080

```
		docker run -p 8080:8080 tomcat
```

On the same host you can run another tomcat application with another port on a different container.

```
		docker run -p 8090:8080 tomcat
```

**13. run - volume mapping**

```
	docker run -v /opt/datadir:/var/lib/mysql mysql
```

this will map the "/opt/datadir" storage on host to the "/var/lib/mysql" inside the container
	
**14. Inspect container**

```
	docker inspect <container-name>
```

**15. Container Logs**

```
	docker logs <container-name>
```

**16. to see the image history**

```
	docker history <image-id>
```

**17. To see the actual disk usage of docker system**

```
	docker system df -v 
```

**18. Create a user-defined bridge network **

```
	docker network create \
		--driver bridge \
		--subnet 182.18.0.0/16 \
		custom-isolated-network
```	

**19. List the network**

```
	docker network ls
```

**20. To remove all the stopped containers**

```
 	docker container prune
```		

**21. Restart containers automatically while system restart**

```
	docker run --name keep-it-here -d -it --restart=always ubuntu
```	
