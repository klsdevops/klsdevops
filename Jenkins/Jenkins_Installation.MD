# Install Jenkins on AWS EC2
Jenkins is a self-contained Java-based program, ready to run out-of-the-box, with packages for Windows, Mac OS X and other Unix-like operating systems. As an extensible automation server, Jenkins can be used as a simple CI server or turned into the continuous delivery hub for any project.


### Prerequisites
1. EC2 Instance 
   - With Internet Access
   - Security Group with Port `8080` open for internet
1. Java v1.8.x 

## Install Java
1. We will be using open java for our demo, Get the latest version from http://openjdk.java.net/install/
   ```sh
   $ yum install java-1.8*
   #yum -y install java-1.8.0-openjdk-devel
   ```
![image](https://user-images.githubusercontent.com/90503660/135739043-3f55aebc-776c-45a7-b7bc-423934914686.png)

1. Confirm Java Version and set the java home
   ```sh
   $ java -version
   $ find /usr/lib/jvm/java-1.8* | head -n 3
   $ export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-<Java version which seen in the above output>
   $ export PATH=$JAVA_HOME/bin:$PATH
    # To set it permanently update your .bash_profile
   vi ~/.bash_profile
   ```
   _The output should be something like this,_
   
   ![image](https://user-images.githubusercontent.com/90503660/135741875-5929bdfe-8573-4554-ab72-688bbdb45d39.png)

## Install Jenkins
 You can install jenkins using the rpm or by setting up the repo. We will set up the repo so that we can update it easily in the future.
1. Get the latest version of jenkins from https://pkg.jenkins.io/redhat-stable/ and install
   ```sh
   $ yum -y install wget
   $ sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
   $ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
   $ yum -y install jenkins
   # Sometimes this installation fails on amazon-linux because of daemonize issue. 
   # Requires: daemonize
   # Then you will have to install epel-release which provides daemonize. For installing epel-release on amazon-linux, follow the below command
   $ sudo amazon-linux-extras install epel
   
   ```
   ![image](https://user-images.githubusercontent.com/90503660/135739171-6d03a52f-fee8-4f22-a6ce-8bc8dab7fe42.png)
   ![image](https://user-images.githubusercontent.com/90503660/135739191-56912119-7fb7-4669-96be-47e4ec008b1e.png)

   ### Error Screenshot: 
   
   ![image](https://user-images.githubusercontent.com/37894194/132466158-8a1944fd-5c73-4bbd-a707-dfa0c8b38771.png)
   
   ### Start Jenkins
   ```sh
   # Start jenkins service
   $ service jenkins start

   # Setup Jenkins to start at boot,
   $ chkconfig jenkins on
   ```
   ![image](https://user-images.githubusercontent.com/90503660/135739216-b9815bda-0e40-416e-a7e3-0329175e86d4.png)

   ### Accessing Jenkins
   By default jenkins runs at port `8080`, You can access jenkins at
   ```
   http://YOUR-SERVER-PUBLIC-IP:8080
   ```
   
   #### Setting up Jenkins console
   * _**Access the Jenkins URL (eg; http://3.22.222.129:8080)**_

	![image](https://user-images.githubusercontent.com/90503660/135739292-1b86962e-b1ca-4721-945f-b5e0cfb2e32b.png)

   * _**Get the Password, copy/paste and click "Continue"**_

	![image](https://user-images.githubusercontent.com/90503660/135739313-0bb1ae0b-9dfa-4c33-af14-c346c0f571cb.png)
	
   * _**Click on "Install suggested plugins"**_
   
   	![image](https://user-images.githubusercontent.com/90503660/135739352-61092956-7c89-4a0d-ad35-d20c54ef4ad6.png)
	
	You would see the default plugins getting installed on the jenkins.
	![image](https://user-images.githubusercontent.com/90503660/135739393-0a54a051-e68f-42eb-bae9-b2d296aea732.png)
	
   * _**Create first admin user**_ ( you can even skip this & continue as admin and setup new users later as well)
   
   	![image](https://user-images.githubusercontent.com/90503660/135739485-d9b6129b-8593-400d-bc9e-596d07d3c5da.png)
	
   * _**Click on the "Save and Finish" button**_
   	
	![image](https://user-images.githubusercontent.com/90503660/135739513-75285e0e-3cca-431a-87e3-0c2df93cd164.png)
	
   * _**Your jenkins is ready now**_
   	
	![image](https://user-images.githubusercontent.com/90503660/135739611-69597669-e6f1-429c-abb9-d23514073090.png)
  
   * _**Start using Jenkins**_
   	
	![image](https://user-images.githubusercontent.com/90503660/135739634-78636e73-5280-473c-90fb-85108a6e8fa7.png)
   
  #### Configure Jenkins
- If you want to change user password
   - `root` > `Configure` > `Password`
   
   ![image](https://user-images.githubusercontent.com/90503660/135739866-e27dc688-132a-4ee9-b81a-f0a8bd8109d0.png)

- Configure `java` path
  - `Manage Jenkins` > `Global Tool Configuration` > `JDK` 

  ![image](https://user-images.githubusercontent.com/90503660/135739905-38a4dfac-bb76-49ad-90f0-59d40328d7e3.png)

  Click on "Add JDK" button
  
  ![image](https://user-images.githubusercontent.com/90503660/135739940-74be7b99-150f-4ee7-98d9-4ecb2556e758.png)

  Since we already have java jdk 8 installed on our machine, just unselect the "Install Automatically" button and provide a Name & Home Path location.
  
  ![image](https://user-images.githubusercontent.com/90503660/135740034-10d77ac3-cfc6-441f-bfc3-f2000f3dba5b.png)

  Click "Apply" and then "Save"
  
- The same way you can configure the other default plugins installed as well (git, maven etc.)
	
	- For each plugin you will have to do an installation of packages on the Jenkins Controller Machine.
	- You can do a manual installation from the Jenkins Controller CLI.

### Test Jenkins Jobs
1. Create “new item”
2. Enter an item name – `My-First-Project`
   - Chose `Freestyle` project
3. Under the Build section
	Execute shell: echo "Welcome to Jenkins Demo"
4. Save your job 
5. Build job
6. Check "console output"

