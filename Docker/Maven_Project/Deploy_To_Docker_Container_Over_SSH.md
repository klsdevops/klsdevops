--- YYY ---

# Now to deploy the war file to a Docker Container we need to follow the below,

1. Create a Dockerfile
2. Edit the Jenkins Job "Deploy_to_docker" and add the docker commands under command execution
3. Execute the job to see the results

## Create a Dockerfile on the Docker Host

```
FROM tomcat:latest
MAINTAINER klsdevops
COPY ./webapp.war /usr/local/tomcat/webapps
```

![image](https://user-images.githubusercontent.com/90503660/138553649-0ac8ef64-41cd-4cb0-ab6a-c48e60f5b822.png)

## Modify the pipeline for executing docker commands

```
cd /home/dockeradmin; docker build -t tomcat-app .; docker run -d --name tomcat-app-container -p 8080:8080 tomcat-app;
```

![image](https://user-images.githubusercontent.com/90503660/138553554-7357b295-b2a2-4637-ad7d-eb73223ea910.png)

## Execute the job & verify the results

![image](https://user-images.githubusercontent.com/90503660/138553890-8399c3a9-174e-40ec-a547-d0bc70d954c9.png)

The job has completed successfully. Now we could verify the Docker Host machine

![image](https://user-images.githubusercontent.com/90503660/138553918-0f58937a-3583-4ae4-80d9-b272cd99d9f4.png)

You could see a container is running

Now access the application from the browser

HTTP-URL/webapp/

![image](https://user-images.githubusercontent.com/90503660/138553935-0d6761d2-30ec-4855-9049-aaec23a726ef.png)

## You could see your tomcat application is up & running.

**NOTE:**
If you try to run the Job again, you would see some issues, and your build would be UNSTABLE

![image](https://user-images.githubusercontent.com/90503660/138554044-3d22dab9-4c49-43bf-bedf-3ee680acf106.png)

We will address these issues in the coming lessons.

