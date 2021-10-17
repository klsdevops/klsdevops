# How to containerize a Python Application ?

## Pre-Requisites
* Docker

Ensure Docker is installed

```
docker --version
```

![image](https://user-images.githubusercontent.com/90503660/137612345-517c80ec-a60c-4b11-a0bb-4127e8b07191.png)


## Launch a Base Container (Ubuntu bsed)
```
docker run ubuntu
```

![image](https://user-images.githubusercontent.com/90503660/137612384-f9d3b37c-f3d2-4cb3-870c-60957f7cfe46.png)

### Now you are inside the container. You can manually configure everything needed for your application inside this container.

#### Update the base packages

```
apt-get update
```

![image](https://user-images.githubusercontent.com/90503660/137612425-77162e26-3e4a-4893-a0bc-a1c74f787c82.png)

#### Install python

```
apt-get install -y python
```

![image](https://user-images.githubusercontent.com/90503660/137612534-27cc1654-ba21-4978-9d14-3bbd327eab34.png)

### Verify you are getting the python prompt

![image](https://user-images.githubusercontent.com/90503660/137612571-9458e96e-83d0-4ad7-bdf5-eb2f3cd63cb0.png)

### Install python pip package

```
apt-get install -y python-pip
```

**NOTE:** Sometimes you might get error while installing python-pip

![image](https://user-images.githubusercontent.com/90503660/137613025-45fd05d6-7b30-4ade-8185-cd2588747711.png)

Then you will have to install python-pip with alternate methods

```
apt-get install -y curl
curl https://bootstrap.pypa.io/pip/2.7/get-pip.py -o get-pip.py
python get-pip.py
```

![image](https://user-images.githubusercontent.com/90503660/137613186-24158433-5a4f-4c74-bf29-a86536abb7fb.png)

#### Install the Flask dependency for the web application

```
pip install flask
```

![image](https://user-images.githubusercontent.com/90503660/137613208-2c97f3b1-fea6-4d40-a25f-15cdbf175085.png)

#### Copy the application source code

```
apt-get install -y vim
```

vi /opt/app.py
```
import os
from flask import Flask
app = Flask(__name__)

@app.route("/")
def main():
    return "Welcome!"

@app.route('/klsdevops')
def hello():
    return 'Happy Learning!'

if __name__ == "__main__":
    app.run()
```

![image](https://user-images.githubusercontent.com/90503660/137613394-f95a0754-2645-454b-9d78-12350f211527.png)

#### Run the application

```
FLASK_APP=/opt/app.py flask run --host=0.0.0.0
```

![image](https://user-images.githubusercontent.com/90503660/137613402-d2b1db88-b78f-4cd7-995b-5352397ee909.png)

#### Verify the application 

You can open a duplicate terminal and access the application locally.

![image](https://user-images.githubusercontent.com/90503660/137613475-2b0b5bbe-c57b-4aba-a578-cb8a51347919.png)

**NOTE:** Since we didn't do any port forwarding while starting the container, it will not be accessible from outside world.


# Containerize your Application

Now you could write a Dockerfile & create an image of your application and make it portable.
You can refer your command history to write the Dockerfile

![image](https://user-images.githubusercontent.com/90503660/137613555-6be8de9c-62b0-4745-aa18-f5bd22b018a5.png)

## The below are the commands we used to setup the application

```
    1  apt-get update
    2  apt-get install -y python
    3  apt-get install -y curl
    4  curl https://bootstrap.pypa.io/pip/2.7/get-pip.py -o get-pip.py
    5  python get-pip.py
    6  pip install flask
    7  apt-get install -y vim
    8  vi /opt/app.py
    9  FLASK_APP=/opt/app.py flask run --host=0.0.0.0
```

## Setup the source code on your Host Machine

```
mkdir sample-python-webapp
cd sample-python-webapp/
cat > app.py
import os
from flask import Flask
app = Flask(__name__)

@app.route("/")
def main():
    return "Welcome!"

@app.route('/klsdevops')
def hello():
    return 'Happy Learning!'

if __name__ == "__main__":
    app.run()
```

![image](https://user-images.githubusercontent.com/90503660/137613823-f94128e2-59df-4765-b1b1-b63023c08daf.png)

## Write your Dockerfile

vi Dockerfile
```
FROM ubuntu
MAINTAINER KLSDEVOPS
RUN apt-get update && \
    apt-get install -y python curl vim 
RUN curl https://bootstrap.pypa.io/pip/2.7/get-pip.py -o get-pip.py
RUN python get-pip.py
RUN pip install flask
COPY app.py /opt/app.py
ENTRYPOINT FLASK_APP=/opt/app.py flask run --host=0.0.0.0
```

![image](https://user-images.githubusercontent.com/90503660/137613831-8d1e3197-708d-4b30-9bf2-bf54ebf5c339.png)

## Build the application image

```
docker build -t sample-python-webapp .
```

![image](https://user-images.githubusercontent.com/90503660/137613962-8a285396-2e81-444e-bbf0-70fad48a5b6a.png)

## Verify the image created

```
docker images
```

![image](https://user-images.githubusercontent.com/90503660/137613971-96bbeaec-89af-4c37-822d-5b8484a85baa.png)

## Launch an application container using this Image

```
docker run -it -d --name sample-webapp -p 8080:5000 sample-python-webapp:latest
```

![image](https://user-images.githubusercontent.com/90503660/137614029-5325a416-0e0c-4ae9-aef1-a81fc0a6f208.png)

## Verify the container status

```
docker ps
```

![image](https://user-images.githubusercontent.com/90503660/137614052-50c207e4-7301-4151-9be4-2875f1ff079b.png)

## Access the application from browser

Open a browser and access it with the HOST-IP:PORT

eg; http://18.220.21.171:8080/

![image](https://user-images.githubusercontent.com/90503660/137614089-b42e2197-d052-4a97-ba8a-8812a41320ef.png)


![image](https://user-images.githubusercontent.com/90503660/137614102-dcfd6edf-3a3c-48ab-a0af-ba05e35007c1.png)

## Now push the image to the Dockerhub

* Tag your image with the registry name
* Login to docker Registry
* push the image to the Registry

```
docker tag sample-python-webapp:latest klsdevops/sample-python-webapp:latest
docker login
docker push klsdevops/sample-python-webapp
```

![image](https://user-images.githubusercontent.com/90503660/137614319-26505ad0-b541-4da2-9933-d4a3d945ad7c.png)

## Verify on the DockerHub

![image](https://user-images.githubusercontent.com/90503660/137617501-6b9ec3b6-984b-429a-b25b-e80c4d94c396.png)

# This is how you will containerize an application and make it portable.

This image can be downloaded to any other machine & can be deployed there.
