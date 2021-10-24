# Integrate Ansible with Jenkins

## We need to enable the SSH connection between Jenkins & Ansible machine (We will be following the same steps we did for the Docker communication)

Go to Jenkins Console -> Manage Jenkins -> Configure System -> Publish over SSH -> SSH Servers -> Add 

![image](https://user-images.githubusercontent.com/90503660/138583367-37081c79-d498-4839-bcf3-6c55467004b0.png)

Provide the connection details

![image](https://user-images.githubusercontent.com/90503660/138583427-33e38650-8cbc-409f-966e-94d7ad7280bd.png)

Go to the Advanced tab and select password authentication & provide password of ansadmin user,

![image](https://user-images.githubusercontent.com/90503660/138583449-14963f24-6039-47a4-8d0f-73fd96d33fdc.png)

Test configuration

![image](https://user-images.githubusercontent.com/90503660/138583481-61dd526f-64d1-43f0-ba46-d1d2f606d7a1.png)

