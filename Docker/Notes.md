# This is some reference note 

Docker can run any OS based on the underlying host machine's kernel.
	eg; On an ubuntu based Host machine, you can run any other flavours of Linux docker containers. But can not run a Windows/macOS container on it.
	
## Docker on windows (for running Linux containers on windows):
**1. Docker on windows using Docker Toolbox (this is a Legacy setup)**
* Install some tools like Oracle Virtualbox or VM workstation & deploy a Linux VM on it. Then install docker on the Linux VM.
* Docker Toolbox contains a set of tools like
  - Oracle Virtualbox
  - Docker Engine
  - Docker Machine
  - Docker Compose
  - Kitematic GUI

	You can simply Download Docker Toolbox executable and install it on a Windows Machine.
  The pre-req for this is
    - 64-bit OS
    - Windows 7 or higher
    - Virtualization is enabled.

**2. Docker Desktop for Windows.(A newer setup)**

This will come with "Microsoft Hyper-V" by default. So it requires the below,
  - windows 10 Enterprise/Professional Edition or windows 2016 server
  - When you install Docker Desktop for windows, the default option is to work with Linux Containers.
  - From 31 August 2021, Docker has announced that professional use of Docker Desktop in large organizations(more than 250 employees OR $10 M revenue) requires users to have a paid Docker Subscription.

You can not have both these options together on a single machine. 

## Docker for windows(for running windows container on windows machine)
  - With windows 2016 server, Microsoft announced support for windows containers.
  - You can now package windows based application into windows docker containers and run them on windows docker host using Docker Desktop for windows.
  - To work with windows containers, you must explicitly configure docker for windows to "Switch to Windows containers" on the Docker Desktop.
  - Container feature should be enabled. (it will automatically enable & reboot your system when you swithc to windows containers)
  - In windows, there are two types of containers
    * Windows Server Container (its similar to the Linux containers where it share the Kernel with the underlying Windows OS)
      - Windows container on native windows server core.

    * Hyper-V Isolation 
      - windows container on an isolated hyper-v kernel.
      - Its for better security options
      - Each container is run within a highly optimized VM guaranteeing complete kernel isolation between the containers and underlying host.

  - Windows have only two base images available.
		* Windows Server Core - Its not a light weight one.
		* Nano Server

      A Nano Server is a headless deployment option for windows. Which runs at a fraction of size of the full OS.(Its as light as an Alpine Image in Linux)

Unlike hypervisors, Docker is not mainly meant to virtualize and run different OS and kernels on the same hardware , The main purpose of Docker is to package and containerize application and to ship them and run it anywhere, any time as many time you want.

## Image
An image is a package or Template.
For creating a Docker Image, you will have to collaborate with the Developers to get the application details

## Docker has two Editions.
* Community
  Is a set of free docker products

* Enterprise
Is the certified and supported container platform that comes with enterprise addons like the image management, image security, universal control plane for managing and orchestrating container run time. It comes with a price.

## Containers:
Containers are not meant to host an OS, infact its meant to run a specific task or process such as to host an instance of a web server or an application server or a database or simply to carry some kind of computation or analysis task.
So, once the task is complete, the container exits. A container only live as long as the process inside it is alive.
  For eg; If the web service inside the container is stopped or a crash then the container exits.
  In other words, if you simply run a container with an ubuntu image, it simply exits as its meant for to be used as a base image for an application. There is no process or application running in it by default. Or probably you could instruct the Docker to run a process with the docker run command.
  
## What am I containerizing?
Application

## How to create my own image?
Dockerfile format:
  **INSTRUCTION**		**argument**
  eg;
  FROM 			ubuntu
  RUN				apt-get update
  
Docker build will generate the image with a layered architecture.
Each line of INSTRUCTION will create a layer with just the changes from the previous layer.
To see the layers, issue the below command
```
docker history <image-name>
```

All the layers are cached. So in case of a failure, it doesn't need to do everything from beginning, instead it can retrieve it from the cache.
Also adding more instructions to your Dockerfile and rebuilding an image is also faster as it can use the layered cache instead of rebuilding from the scratch.
The image layers are read only. Once you create an image, you can not alter it or write anything to it. But when you launch a container with it, it will bring an additional layer "container layer" which is a writable layer. Here we can alter the image and commit the new changes. The life of this layer is till the container is live.

## CMD v/s ENTRYPOINT

## Docker Registry:
The Registry is a stateless, highly scalable server side application that stores and lets you distribute Docker images. 
Docker Images are stored in a registry.
Image Name:  <registry-name>/<account-name>/<image-name>:<tag>

If you don't specify a registry name while pulling the docker image, by defualt it pull from the DockerHub(docker.io).

  docker.io/klsdevops/sample-python-webapp:latest

Always login to the registry before pulling or pushing to a private registry,
```
	docker login <registry-name>
	userID:
	Password:
```

**Deploy a private registry:**

You can use the docker registry image to setup a local private registry;
```
docker run -d -p 5000:5000 --name registry registry:2
docker image tag my-image localhost:5000/my-image
docker push localhost:5000/my-image
```

To pull this image from another machine,
```
  docker pull <IP-ADDR>:5000/my-image
```

With specific storage requirements,
```
docker run -d \
	  -p 5000:5000 \
	  --restart=always \
	  --name registry \
	  -v /mnt/registry:/var/lib/registry \
	  registry:2
```

## Docker Engine:
Its simply a host with docker installed on it.
When you are installing docker on a linux host, you are installing the below components,
1. **Docker CLI** - The command line interface. Its not necessary to be on the same host, it could be on another machine/laptop and still can talk to a remote docker engine. Just use the "-H=<remote-engine-IP:port>. 
  eg; docker -H=192.168.2.12:2375 run nginx
2. **REST API Server** - An API interface that programs can use to talk to the deamon and provide instructions.
3. **Docker Deamon** - A background process that manages docker objects such as images, containers, volumes & networks
  
The docker CLI uses the REST API to interact with the Docker Deamon.
Docker uses namespaces to isolate workspace.

## Docker storage:

For data persistancy, we will have to create docker volumes and mount this volume to the container,
```
docker volume create data_volume
docker volume ls	
docker run -v data_volume:/var/lib/mysql mysql
```
Even if you don't create a volume explicitly, while you try to map a volume to a container it will automatically create a volume in the background and then map it.
```
docker run -v data_volume2:/var/lib/mysql mysql
```

Actual command:
```
docker run -v data_volume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql
docker exec -it mystifying_golick bash
mkdir /data/mysql
docker run -v /data/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql
```

Using -v is old method, now its "--mount"
  
```
docker run \
	--mount type=bind,source=/data/mysql,target=/var/lib/mysql mysql \
  -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql
```

Docker uses storage drivers to enable layered architecture. The different types of storage drivers are as below,
* AUFS
* ZFS
* BTRFS
* Device Mapper
* Overlay
* Overlay2

The selection of storage driver depends on the underlying OS. 
  eg; with ubuntu, the default storage driver is aufs. The aufs storage driver Was the preferred storage driver for Docker 18.06 and older, when running on Ubuntu 14.04 on kernel 3.13 which had no support for overlay2.
  For fedora/centos, device mapper will be a better option. devicemapper was the recommended storage driver for CentOS and RHEL, as their kernel version did not support overlay2. However, current versions of CentOS and RHEL now have support for overlay2, which is now the recommended driver.
  Docker will choose the best driver available automatically based on the OS.
    overlay2 is the preferred storage driver for all currently supported Linux distributions, and requires no extra configuration.

## Docker Networks:
When you install Docker, by default it creates three networks;
  * Bridge 
  * Host
  * None

  **Bridge:**
    - The default network a container gets attached to.
    - If you would like to associate the container with any other network, you need to explicitly specify that network information using the network command parameters.

```
docker run ubuntu --network=none
docker run ubuntu --network=host
```
  - The Bridge network is a private internal network created by Docker on the host.
  - All containers attached to bridge network gets an internal IP address usually in the range 172.17 series. The containers can communicate between each other using this internal IP. To access any of these containers from outside world, map the ports of these containers to ports of on the Docker Host.
  
  **Host:**
  - Another way to access the containers externally is to associate the container to the host network.
  - This takes out any network isolation between the docker host and the docker container.
    For eg; 
  	If you want to run a web server on port 5000 in a web container, it is automatically accessible on the same port externally without requiring any port mapping as the web container uses the host network.
  - With host network, you can not run multiple web containers on the same host with the same port(5000) as the ports are common to all containers in the host network.
    
  **None:**
  - With the none network, the containers are not attached to any network and doesn't have any access to the external network and to other containers.
  - The containers run in an isolated network.
  
  **User-Defined Networks:**
  - By default docker creates only one internal bridge network, but we could create our own internal network using the below command;
  
```
docker network create \
  --driver bridge \
  --subnet 182.18.0.0/16 \
  custom-isolated-network
 
docker network ls
```
there is no guarantee that a container would get the same IP after a reboot.

## Inspect Network:
```
docker inspect <container-name>
```
  - Containers can reach each other by using their names.
  - Docker has a built-in DNS server which helps the containers to resolve each other using the container name.
  - The built-in DNS server always runs at the address 127.0.0.11
