# Tomcat installation on EC2 instance

### Pre-requisites
1. EC2 instance with Java v1.8.x 

  #### Java 1.8.x Installation
  ```
  $ yum install java-1.8*
  #yum -y install java-1.8.0-openjdk-devel
  ```
  ### Set the JAVA_HOME and PATH
  ![image](https://user-images.githubusercontent.com/90503660/135748247-df89e77f-c1f0-4cc6-a1c4-1f5489515834.png)

### Install Apache Tomcat
1. Download tomcat packages from  https://tomcat.apache.org/download-80.cgi onto /opt on EC2 instance
   > Note: Make sure you change `<version>` with the tomcat version which you download. 
   ```sh 
   # Create tomcat directory
   cd /opt
   wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.71/bin/apache-tomcat-8.5.71.tar.gz
   tar -xvzf /opt/apache-tomcat-<version>.tar.gz
   ```
   
   ![image](https://user-images.githubusercontent.com/90503660/135748071-908c3555-81b7-4274-b84a-4cff7f375fcc.png)

1. give executing permissions to startup.sh and shutdown.sh which are under bin. 
   ```sh
   chmod +x /opt/apache-tomcat-<version>/bin/startup.sh 
   chmod +x /opt/apache-tomcat-<version>/bin/shutdown.sh
   ```
   > Note: you may get below error while starting tomcat incase if you dont install Java   
   `Neither the JAVA_HOME nor the JRE_HOME environment variable is defined At least one of these environment variable is needed to run this program`
   
   ![image](https://user-images.githubusercontent.com/90503660/135748132-52136cdb-c589-42fd-a7ae-8597f8fff53e.png)

1. create link files for tomcat startup.sh and shutdown.sh 
   ```sh
   ln -s /opt/apache-tomcat-<version>/bin/startup.sh /usr/local/bin/tomcatup
   ln -s /opt/apache-tomcat-<version>/bin/shutdown.sh /usr/local/bin/tomcatdown
   tomcatup
   ```
   ![image](https://user-images.githubusercontent.com/90503660/135748467-fec5ff28-e90b-49ac-880b-c3392a3a1e7e.png)
   ![image](https://user-images.githubusercontent.com/90503660/135748573-7399b33a-bede-4bce-843e-ee5bd983a96e.png)
   ![image](https://user-images.githubusercontent.com/90503660/135748589-1a1a2dd6-fe36-41e2-bdcd-782163887717.png)

  #### Check point :
access tomcat application from browser on port 8080  
 - http://<Public_IP>:8080
 
   ![image](https://user-images.githubusercontent.com/90503660/135748660-dd620fe7-fbf7-41d2-9a79-9e8d29ac9c25.png)

  Using unique ports for each application is a best practice in an environment. 
  But tomcat and Jenkins runs on ports number 8080. Hence lets change tomcat port number to 8090. (Since we are deploying in a different server than Jenkins, its not required for our LAB)
  Change port number in conf/server.xml file under tomcat home
  
   ```sh
 cd /opt/apache-tomcat-<version>/conf
# update port number in the "connecter port" field in server.xml
# restart tomcat after configuration update
tomcatdown
tomcatup
```

![image](https://user-images.githubusercontent.com/90503660/135748762-7f272fcb-9fe1-49b5-a0ef-9d29e79543c1.png)

![image](https://user-images.githubusercontent.com/90503660/135748808-20e0c5cf-7323-4b82-8b66-f56934166ae6.png)

![image](https://user-images.githubusercontent.com/90503660/135748831-6b2f004d-4995-4f81-9064-618bc21b24a0.png)

**NOTE:** Since you are using an EC2 instance, you will have to open 8090 port in the inbound rules of Security Group.

#### Check point :
Access tomcat application from browser on port 8090  
 - http://<Public_IP>:8090

![image](https://user-images.githubusercontent.com/90503660/135749131-2949d3ce-9900-4ea8-8c05-254c99bb06dc.png)


1. now application is accessible on port 8090. but tomcat application doesnt allow to login from browser. 
    
   When you click on the "Managed Apps" button, you will get the below error
   
   ![image](https://user-images.githubusercontent.com/90503660/135749198-6f9e7ca0-3ef2-4326-a2e6-5bfb976f27e8.png)

   changing a default parameter in context.xml does address this issue
   
   ```sh
   #search for context.xml
   find / -name context.xml
   ```
   
   ![image](https://user-images.githubusercontent.com/90503660/135749229-b77d4860-d284-40f4-9f15-ed570cac933a.png)

2. above command gives 4 context.xml files. comment (<!-- & -->) `Value ClassName` field on files which are under webapp directory. 
After that restart tomcat services to effect these changes. 
At the time of writing this lecture below 2 files are updated. 
   ```sh 
   /opt/tomcat/webapps/host-manager/META-INF/context.xml
   /opt/tomcat/webapps/manager/META-INF/context.xml
   
   # Restart tomcat services
   tomcatdown  
   tomcatup
   ```
   ![image](https://user-images.githubusercontent.com/90503660/135749280-e23ed0ad-be7b-42ac-bd17-00adbb119b74.png)
  
    ![image](https://user-images.githubusercontent.com/90503660/135749297-504ea706-da79-41ac-a9c5-c9bd38a193f6.png)

    ![image](https://user-images.githubusercontent.com/90503660/135749328-2d4ad349-0a1b-4ff1-a357-37079b86b9b8.png)

3. Update users information in the tomcat-users.xml file
goto tomcat home directory and Add below users to conf/tomcat-users.xml file
   ```sh
	<role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<role rolename="manager-jmx"/>
	<role rolename="manager-status"/>
	<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
	<user username="deployer" password="deployer" roles="manager-script"/>
	<user username="tomcat" password="s3cret" roles="manager-gui"/>
   ```
   
   ![image](https://user-images.githubusercontent.com/90503660/135749409-aa9f4058-34e0-47a5-8b33-ffdd96992093.png)**

**NOTE:** You could even encrypt this password as part of security.
To encrypt the password, 

Step 1: Edit  server.xml

-add the diggest option to Realm line at server.xml which is located under conf directory.


Before:
```
<Realm className="org.apache.catalina.realm.LockOutRealm">
```
After:
```
<Realm className="org.apache.catalina.realm.LockOutRealm" digest="md5">
```

![image](https://user-images.githubusercontent.com/90503660/156538974-d1aa29c9-b363-4d76-9bdb-3a0aad1b0a2e.png)

Step 2: Create  encrypted password

```
cd /opt/apache-tomcat-8.5.76/conf
vi server.xml
```
![image](https://user-images.githubusercontent.com/90503660/156539212-b26d94c9-27f8-4def-807e-10ea22f5cd35.png)

Step 3:Replace the user's password to an encrypted one.

-Replace value of user's "password" attribute in your tomcat-users.xml to <ENCRYPTED_PASSWORD>

	
```
cd /opt/apache-tomcat-8.5.76/conf
vi tomcat-users.xml
```

![image](https://user-images.githubusercontent.com/90503660/156539410-cbeae114-99fc-4794-9df6-302b8fd2c302.png)


4. Restart serivce and try to login to tomcat application from the browser. User credentials for the user "tomcat". This time it should be Successful

	![image](https://user-images.githubusercontent.com/90503660/135749417-9c943043-e3a7-4070-90d6-6d68e25b254a.png)
	
	![image](https://user-images.githubusercontent.com/90503660/135749462-1a18e5aa-5237-4d33-8206-ddad5a23cc6c.png)
	
	![image](https://user-images.githubusercontent.com/90503660/135749477-d025e6b5-f61d-40dc-af4c-92a3d372100f.png)


