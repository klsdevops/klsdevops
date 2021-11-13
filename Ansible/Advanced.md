# Ansible Advanced:
## File Separation:
### Variables File Separation:
#### Host Variables:
Create a folder "host_vars" in the same level where the playbook.yml file is kept. Its important to name the folder as "host_vars" because that's the folder that ansible looks at to find out whether there is a variable file for a particular server.

create a file inside this "host_vars" folder with the same name as of the server (eg; app_server.yml). It is important to name the file with the same name of the server cause ansible automatically reads the values from this file and associates them with the hosts.

Move the variables defined in the inventory file to this file
```
			vi host_vars/app_server.yml
				ansible_ssh_pass: Passw0rd 
				ansible_host: 192.168.1.14
```

You need to keep separate variable files for each servers in your inventory the same way.
			
#### Group Variables:
For group variables, there must be a folder called "group_vars".
So, if you are grouping your servers in your inventory, then instead of keeping separate variable files for each server under "host_vars", you could create a folder "group_vars" and keep the variables in a file with the same name as your server group(eg; db_and_web_servers.yml).
In our playbook example, you could separate those variables defined in the playbook to this variable file under group_vars folder.(remove it from playbook and keep it in a separate "group_vars/db_and_web_servers.yml" file.)
```
			vi group_vars/db_and_web_servers.yml
				db_name: employee_db
				db_user: db_user
				db_password: Passw0rd
```

### Include files:
You could separate out the common tasks to separate files and include those files in different playbooks with include statements, so that you could re-use those code.

For eg; divide your database deployment tasks & web deployment tasks in to two separate files under a folder "tasks"
```
				vi tasks/deploy_db.yml
					-name: Install Dependencies
						
					-name: Install MySQL Database
					
					-name: Start MySQL Service
					
					-name: Create Application Database
					
					-name: Create Application DB User
					
				vi tasks/deploy_web.yml
					
					-name: Install Python Flask Dependencies
					
					-name: Copy Web-Server code
					
					-name: Rub Web-Server
```

Now you could use these files in your playbook
```
				-
					name: Deploy Web Application
					hosts: app_server
					tasks:
					- include: tasks/deploy_db.yml
					
					- include: tasks/deploy_web.yml
```
You could re-use these include files anywhere in your project.
	
## Roles:
Roles are the recommended way of developing a playbook in ansible. Roles helps us organize our project in a standard structure.
We could use roles within our project and share our work with open community through GitHub or Ansible Galaxy.
When you create a role, it automatically create a folder structure.

Syntax: ansible-galaxy init my-role

Once roles are created, you could simply use the roles in your playbook.
```
		-
			name: Deploy Web Application
			hosts: app_server
			roles:
			- webserver
			- my-role
```

You dont need to use any include commands when you are using the roles.
You can import existing roles from the ansible galaxy community as well.

Syntax: 
```
ansible-galaxy import <role name>
```

You can search for any roles in the ansible-galaxy community.
Syntax: 
```
ansible-galaxy search <keyword>
```

eg; ansible-galaxy search mysql

Its not mandatory to use "ansible-galaxy" command to create roles. You could create the same structure by your self as well. But its easy to use ansible-galaxy for creating the roles.

When you create a role, there will be a README.md file created by default. You should make sure that you are updating details about the role you are creating in this README.md file.
	
## Asynchronous Actions:
When you want to execute a task and check on it later, you could use asynchronous actions.

eg;
```
		-
		name: Deploy Web Application
		hosts: app_server
		tasks:
			- command: /opt/monitor_webapp.py
			  async: 360
			  poll: 60
```

The async directive tells ansible that this is an asynchronous task, so kick it off and check on it later. So we would use async directive to specify the maximum time we would expect the task to execute, Say 6mins in our example.

By default, ansible checks the status every 10 seconds. If you want to change it, use the poll directive.
* async -> How long to run.
* poll -> how frequently to check.

So in this case, the ansible execute this task & wait for 6 mins to proceed with the next tasks.
So if you want to execute both tasks parallely, you need to specify the poll value as '0'

```
		-
		name: Deploy Web Application
		hosts: app_server
		tasks:
			- command: /opt/monitor_webapp.py
			  async: 360
			  poll: 0
			 
			- command: /opt/monitor_db.py
			  async: 360
			  poll: 0
```

In this case, ansible will go ahead with the next task. However immediately after kicking off the second monitoring task ansible will exit.

Here, we haven't done anything to make ansible wait for the task to finish at the end. In order to do that we must first register the results of this tasks to a variable.

And then we are going to have a new task to the end called check status of the task.
```
		-
		name: Deploy Web Application
		hosts: app_server
		tasks:
			- command: /opt/monitor_webapp.py
			  async: 360
			  poll: 0
			  register: webapp_result
			 
			- command: /opt/monitor_db.py
			  async: 360
			  poll: 0
			  register: db_result
			
			- name: Check status of tasks
			  async_status: jid={{ webapp_result.ansible_job_id }}
			  register: job_result
			  until: job_result.finished
			  retries: 30
			
			- name: check status of database monitor task
			  async_status: jid={‌{ db_result.ansible_job_id }}
			  result: job_result
			  until: job_result.finished
			  retries: 30
```

If second task is already finished (ie. until condition is satisfied) Ansible will exit the playbook run immediately or else it will check for the until condition to be successful with maximum of 30 retries and default delay of 5 seconds between each retry.

Note: all the modules do not support async

* async_status -> Check the status of an async task

## Strategy:
### Linear:

The default strategy in ansible is Linear Strategy. Which means, it executes tasks parallely on multiple servers and goes to the next task and so on.
With the linear strategy all hosts will run each task before any host starts the next task.

#### Free:
Another strategy in ansible is "Free". You could enable this with the "strategy" directive.
eg;
```
			-
				name: Deploy web application
				strategy: free
				hosts: web_servers
				tasks:
```
In this case, each server runs all of its tasks independent of the other server and does not wait for the task to finish on the other servers. So each server can go right to end as fast as it can without bothering about any of the other servers.

#### Batch:
Also we have another directive "serial" where you could specify at a time how many target servers needs to be processed.
Say for eg; if you have 5 target machines & you want to execute playbook only 3 servers at a time, and the other 2 servers after that, then you could mention like below in your playbook.
eg;
```
			-
				name: Deploy web application
				serial: 3
				hosts: web_servers
				tasks:
```
It will run 3 servers in a batch.
So ansible run 3 servers first and once that finishes, ansible proceeds to run on the next batch.

The serial directive has some advanced use cases.

For example you could run the play against 2 servers first, then 3 in the next round and then the last 5 together by providing an array as input to the serial directive. This is really usefull for "Rolling Updates".
**Task**: Update serial directive to use an array instead of a value. Provide 2,3,5 as values.
eg;
```
			-
				name: Deploy a web application
				hosts: app_servers
				serial:
					- 2
					- 3
					- 5
				tasks:
```

You have additional options such as using a "percentage".
So if you say 25% instead of 3, it will run on the 25 percentage of all the servers.
eg;
```
			-
			  name: Deploy a web application
			  hosts: app_servers
			  serial: 20%
			  tasks:
```
You can also create your own custom strategy by developing a strategy plugin.

How many servers ansible can talk to at a time?
Ansible uses parallel processes or forks to communicate with remote hosts. By default, ansible can create 5 forks at a time and this is defined in the ansible configuration file.
```
			vi ansible.cfg
			forks = 5
```

You could modify this value to as much as you like w.r.t the resources(cpu,memory, n/w bandwidth etc.) you have for this operation.

## Error Handling:
### For a single server scenario:
While a playbook executes, it completes one task and then continues to the next. But during the execution if it fails, the play exits.
Say for eg; if you have 5 tasks each to run on the server, by default it executes all the tasks on the server. In between if it fails at 3rd task, then ansible exit the play. Its okay for a single server scenario.

### For multiple servers scenario:
What happens when there are multiple servers. By default, its linear execution and it executes tasks parallely on all the servers.
So if in between any tasks fails, ansible takes that server out of the list and continues to execute the remainder of the tasks accross all the other healthy and available servers.
Ansible will make an attempt to complete as many servers as possible.

If you want ansible to exit the play even if any tasks fails on one server, add an option "any_errors_fatal" on the playbook.
eg;
```
		-
		  name: Deploy a web application
		  hosts: app_servers
		  any_errors_fatal: true
		  tasks:
```

### Ignore Erros:
You could add "ignore_errors: yes" to ignore the errors and continues with the other tasks.
For eg; you want to send a notification mail after some tasks, and if in case of a smtp issues this mail task fails, you still want to continue with the other tasks, you could use this option.

eg;
```
		-
		  name: Deploy a web application
		  hosts: app_servers
		  any_errors_fatal: true
		  tasks:	
			- mail:
				to: abcd@xyz.com
				subject: Deployment completed
				body: web server deployment is completed.
			  ignore_errors: yes
```

### Fail on condition:
If you want your play to fail on satisfying some conditions, you could use "failed_when" option.

eg; If you want to exit the play after checking the log file and you find an ERROR on it,
```
			-
			  name: Deploy a web application
			  hosts: app_servers
			  any_errors_fatal: true
			  tasks:	
				- mail:
					to: abcd@xyz.com
					subject: Deployment completed
					body: web server deployment is completed.
				  ignore_errors: yes
				  
				- command: cat /var/log/server.log
				  register: command_output
				  failed_when: "'ERROR' in command_output.stdout"
```

## Ansible Vault:

**What is Vault?**
Ansible Vault helps us to store this data in an encrypted format.

Use the "ansible-vault" command and run the "ansible-vault encrypt inventory.txt" command. This will encrypt the "inventory.txt" file.
Now, we need to use the "ask-vault-pass" option while running our playbook.
```
ansible-playbook playbook.yml -i inventory.txt ask-vault-pass
```

This will prompt for the vault keyphrase(the one you have provided while encrypting the inventory with ansible-vault). In order to avoid this, you could have the vault password stored in a file and have that file passed in as a value to -vault password file option.
```
ansible-playbook playbook.yml -i inventory.txt -vault-password-file ~./vault-pass.txt
```
To view the contents of an encrypted file,

```
ansible-vault view inventory.txt
```
To create an encrypted file, 
```
ansible-vault create inventory.txt
```

Ansible Vault us used only in command line. So we have no coding to be done in our playbook. Just while executing the playbook, we provide the option "ask-vault-pass".

## Dynamic Inventory:
You need to have custom python scripts for setting up dynamic inventory.

## Modules:
Modules are each item in the tasks list that perform an actual operation or a check.
There are lot of built in modules available in ansible which are ready to use. These are developed with some python code.

### Custom Module:
In order to develop a custom module, we have to develop a custom python script.
		
