# Alternate method to create a CICD pipeline with dockerizing the application

Before running from jenkins "Execute Shell" , make sure that the docker group is added to the jenkins user

![image](https://user-images.githubusercontent.com/90503660/138393576-f4902bcf-41a2-4971-980e-dd256d8db98a.png)

and restart the jenkins services

![image](https://user-images.githubusercontent.com/90503660/138393798-1a59b626-d0e8-4544-abd6-55b1cc91d3c4.png)

otherwise you would see the below error;

![image](https://user-images.githubusercontent.com/90503660/138393644-dec156df-2c46-42ef-8b2e-38f2119652b7.png)

# Instead of using the "execute Shell" method & writing docker commands in it, you could use docker plugins

## Install "Cloudbees Docker Build and Publish" plugin

![image](https://user-images.githubusercontent.com/90503660/138508917-8dff997b-6201-4b7f-bca2-6a8845a22abf.png)

## Now use the "Docker build & Publish" option from the "Add post Build Step"

![image](https://user-images.githubusercontent.com/90503660/138509316-0c198500-cd83-4a57-9ca7-07b82040dc62.png)

![image](https://user-images.githubusercontent.com/90503660/138510761-f27b4c8a-161e-4b70-9af9-bc58aff70052.png)

