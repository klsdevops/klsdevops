# Adding a Jenkins Agent Node

  The Controller Machine is the central, coordinating process which stores configuration, loads plugins, and renders the various user interfaces for Jenkins.
  An agent is typically a machine or container that connects to a Jenkins Controller Machine and is designed to perform the tasks when directed by the Controller.
  
  For a small project with relatively small team, a Jenkins Monolithic installation is sufficient. As your requirements enhances, it often become a necessity to scale up your infrastructure as well. Jenkins provides a way to handle this with a concept of "Controller to Agent connection". Instead of running all the jobs on a monolithic jenkins machine and serving the UI at the same time, we can add multiple agents which can handle the execution of jobs while the Controller serves the Jenkins UI and acts as a control Node.
  
## Pre-requisites:
  1. A Jenkins Controller Node
  2. A Jenkins Agent Node
  3. Java JDK 1.8.x
  4. A user on the Agent Node (eg; jenkins)
  5. For the AWS EC2 servers, we need to allow Password based authentications
 
## Launch a new Jenkins Agent Node

![image](https://user-images.githubusercontent.com/90503660/135787917-7e85cba0-3abf-4aca-af43-537efbe721b0.png)

## Install Java JDK 1.8.x on the Agent Node

![image](https://user-images.githubusercontent.com/90503660/135794751-dd9c08cf-ac19-47ae-8313-9e2c85ef06b7.png)

## Add jenkins user & set password
```
$ useradd -d /var/lib/jenkins jenkins
$ passwd jenkins
```

![image](https://user-images.githubusercontent.com/90503660/135794852-ac271763-2011-46b4-9cb5-a8fe18b16f4c.png)

![image](https://user-images.githubusercontent.com/90503660/135796544-74b4a029-7084-4078-864e-565159a52df6.png)

## Allow password based authentications
```
$ vi /etc/ssh/sshd_config
#Make the PasswordAuthentication to yes

#After saving the file, Restart the sshd service
$systemctl restart sshd
```

![image](https://user-images.githubusercontent.com/90503660/135795242-3d41dfe1-9f44-4f79-83aa-b4da929cd981.png)

![image](https://user-images.githubusercontent.com/90503660/135795365-79c0c01a-3020-4ab7-bf35-cc005e5cc531.png)

## Setting up the Node on the Jenkins Console
### On the Jenkins Console, click on "Manage Jenkins" -> "Manage Nodes"

![image](https://user-images.githubusercontent.com/90503660/135795562-53c53802-895c-41bf-8d47-d2e8a50458bd.png)

### Click on "New Node"

![image](https://user-images.githubusercontent.com/90503660/135795628-860aa8ba-9e92-4604-bf78-7320eb1e0b33.png)

![image](https://user-images.githubusercontent.com/90503660/135795705-52aee4de-458a-49ad-b1a8-279a913dc895.png)

### On the next screen, provide the Agent Details

![image](https://user-images.githubusercontent.com/90503660/135796125-0be60208-421a-4d1e-baae-9c64a97769d1.png)

### Select a launch method, here we are selecting "Launch agents via SSH"

![image](https://user-images.githubusercontent.com/90503660/135796259-10b67507-f8f8-4578-9896-93110e8b06e1.png)

We need to add the credentials of the "jenkins" user we created on the Agent machine in the earlier step.

![image](https://user-images.githubusercontent.com/90503660/135796996-0bbd5e1f-a0bf-4984-813a-7bf83becb14f.png)

### Once the credentials are added, select the same credentials from the dropdown list,
### Also, you need to select "Hostkey verification strategy" as "Non verifying"

![image](https://user-images.githubusercontent.com/90503660/135797174-7bd99b55-0588-41e5-801d-4e0f6ffd2978.png)

### Now press the "Save" button & wait for the Agent to be available

![image](https://user-images.githubusercontent.com/90503660/135797252-841329e4-fdfd-4da3-9d86-4b3b8500e5ed.png)

### You can click on the "Logs" to see the Agent connectivity status
![image](https://user-images.githubusercontent.com/90503660/135797343-c72dfc0f-507a-44fb-8859-fbd145c2a4d0.png)

![image](https://user-images.githubusercontent.com/90503660/135797291-1b26a22f-fea0-4251-aa52-aa41fbf99804.png)

### Now you could see the Agent is ONLINE

![image](https://user-images.githubusercontent.com/90503660/135797397-8957ed1a-500e-4613-a619-d246521e3106.png)

## Do a test job using the Agent Machine

### Go to Jenkins dashboad and create a "new item" & select a "Freestyle Project"

![image](https://user-images.githubusercontent.com/90503660/135797546-bb989e60-9eba-4327-a657-06a736019114.png)

### From the General tab, select the "Restrict where this project can be run" checkbox and provide the Label of Node where you want to run the build.

![image](https://user-images.githubusercontent.com/90503660/135798064-72acfd08-2fc1-484a-8853-eb6474df26b7.png)

### Select the "Execute Shell" from the "Add Build Step" Dropdown list and run some shell commands there(we are running the command `hostname` so that we can see on which host it is getting executed.

![image](https://user-images.githubusercontent.com/90503660/135797798-0f1c7dbc-8a75-408c-bd9d-54450dd28241.png)

### Now run a build job and verify the console output to see on which machine this has executed

![image](https://user-images.githubusercontent.com/90503660/135798212-0ffc4888-c366-4532-b073-67c5996681db.png)


