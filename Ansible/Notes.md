# Ansible Controller:
Ansible controller machine can only be a Linux Server as of now, however windows machines can be a target machine.
  	
# Ansible Inventory:
To establish connectivity from Ansible Controller to Ansible clients,
1) SSH for Linux
2) Powershell Remoting for Windows

This is how ansible is agentless. Agentless means, you don't need to install any additional softwares on the target machines.
A simple SSH connectivity would be suffice Ansible needs.
Information about the target systems is stored in an inventory file.
If you don't create a new inventory file, Ansible uses the default inventory file located at /etc/ansible/hosts.
The inventory file is an INI like format.
Its simply a number of servers listed one after the other.
```
server1.domain.com
server2.domain.com
server3.domain.com
```

You can also group different servers together.
```
[web]
server1.domain.com
server2.domain.com
server3.domain.com
```

You can have multiple groups defined in a single inventory file
```
[web]
server1.domain.com
server2.domain.com
server3.domain.com

[db]
server4.domain.com
server5.domain.com

[clients]
server6.domain.com
server7.domain.com
server8.domain.com
```
## Inventory parameters
- ansible_host				FQDN/IP address
- ansible_connection		ssh/winrm/localhost			defines how to connect to the target server
- ansible_port				22							which port to connect to
- ansible_user				root/Administrator			User to make remote connection
- ansible_ssh_pass			Password					ssh password for linux

Disable host key checking in the ansible.cfg file. (otherwise ssh will fail while you try an ansible ping test). To avoid this situation, its recommended to use SSH Key based connectivity for ansible(rather than a userid/password based connectivity) in the production environment.

# What is YAML ?
A YAML file is used to represent data.
All ansible playbooks are written in YAML.
A key-value pair separated by a column ":"
```
Fruit: Apple
Car: Benz
```
Here the keys are "Fruit & Car" and the values are "Apple & Benz"
Note: You must have a space after the ":"
## Array/List
```
Fruits:
- Apple
- Orange
- Mango

Cars:
- Benz
- Audi
- Lamborghini
```
The dash "-" indicates that its an element of an array.

## Dictionary
```
		Apple: 
			Calories: 85
			Fat: 0.5g
			Carbs: 20g
		
		Orange:
			Calories: 105
			Fat: 0.2g
			Carbs: 10g
```

A dictionary is a set of properties grouped together under an item.
An example for a list containing Dictionaries containing lists,
```
		Fruits:
			-	Apple: 
					Calories: 85
					Fat: 0.5g
					Carbs: 20g
		
			-	Orange:
					Calories: 105
					Fat: 0.2g
					Carbs: 10g
```

Its a list of fruits containing elements of list as Apple & Orange. Each of these elements are further dictionaries containing nutrition information.

A dictionary is an "Unorderd Collection" where as a List is an "Ordered Collection".
The below dictionaries are same though the dictionary item order is different,

```
		Apple: 
			Calories: 85
			Fat: 0.5g
			Carbs: 20g
			
		Apple: 
			Calories: 85
			Carbs: 20g
			Fat: 0.5g
```
But when you define a List/Array, the order matters. The below are not the same,

```
Fruits:
- Apple
- Orange
- Mango
	
Fruits:
- Mango
- Orange
- Apple
```

# Ansible Playbooks
A set of instructions we define ansible to perform
A playbook is a single YAML file.
A play defines a set of tasks to be run on the hosts.

To run a playbook
```
ansible-playbook playbook.yml
```
Ansible command

```
ansible all -m ping -i inventory.txt
```
To check your yaml syntax
www.yamllint.com

Install ATOM IDE
Install the linter-js-yaml packages for checking yaml syntax errors on your IDE.
```
C:\Users\KLSDEVOPS>apm install linter-js-yaml
Installing linter-js-yaml to C:\Users\KLSDEVOPS\.atom\packages done

C:\Users\KLSDEVOPS>
```
Install "remote sync" package for syncing local changes to your remote(GITHUB, Ansible Controller Server etc.)
```
C:\Users\KLSDEVOPS>apm install remote-sync
Installing remote-sync to C:\Users\KLSDEVOPS\.atom\packages done

C:\Users\KLSDEVOPS>
```

When you run a playbook, you will see different status like "ok" and "changed".
  changed => the task has been executed successfully and made changes on the target machine.
  ok => the task is executed and it really didn't make any changes on the target machine as the changes are already available on the target machine.

So ideally, the ansible is gonna make any changes only when it is needed.
	
# Ansible Modules
```
system
   examples:
     user 		-> modifying users/groups on a system
     group
     hostname	
     ping
     service		-> starting/stopping/restarting a system service

command			-> command modules are used to execute commands or scripts on a host.

files			-> File modules helps to work with files.
   examples:
      copy		-> copy module to copy a file from src to dest
      archive		-> archive/unarchive compressed files
      unarchive
		
database		-> helps in working with databases like mongodb, MySQL, PostgreSQL etc.

cloud			-> Has different collection of modules for various cloud providers such as aws, gcp, azure etc.
    Amazon
    Azure
    Docker
    Google

windows			-> windows modules to work on the windows environment
    win_copy	-> to copy files
    win_command	-> to execute windows commands
    win_ping
    win_service
```

# Ansible Variables
Stores information that varies with each hosts.

```
vars:
   key: value
   
To use the variable,
   '{{ key }}'
```

# Ansible Conditionals

when: << condition >>

eg;
```
   when: ansible_os_family == "Debian"
```

We usually use this condition when we need to install packages on multiple hosts depending on the Operating System.
Depending on the OS, ansible needs to decide whether to use "apt" or "yum" for that particular machine.

# Ansible Loops
loop:
  - one
  - two
  - three

To use the loop values,
  {{ item }}
  
eg;

```
tasks:
  - user: name='{{ item.name }}' state=present uid='{{ item.uid }}'
    loop:
      - name: joe
        uid: 100
      - name: raju
        uid: 101
      - name: moydu
        uid: 102
```

Another method of loop is with "with_*" directives,
eg;
```
  with_items:
    - joe
    - michael
    - george
```

example playbook:
```
	-
    name: 'Install required packages'
    hosts: localhost
    vars:
        packages:
            - httpd
            - binutils
            - glibc
            - ksh
            - libaio
            - libXext
            - gcc
            - make
            - sysstat
            - unixODBC
            - mongodb
            - nodejs
            - grunt
    tasks:
        -
            yum: 'name={{ item }} state=present'
            with_items: '{{ packages }}'
```

# Ansible Roles

* You can share the common ansible tasks using roles.
* The primary purpose of the role is to make your work reusable.
* Roles introduce a set of best practices that must be followed to organize all tasks into a task directory, all variables used by these tasks into a vars directory, any default values goes into the defaults directory etc.
* Basically, roles gives you a folder structure which is well organized.
* To get started with Roles, first you need to create the directory structure, you could use ansible-galaxy for doing it.
* Use the "ansible-galaxy init" command to initialize and create a skeleton of your directory structure.
* Roles can be kept under each project directory or it can be kept under default "/etc/ansible/roles" directory.
* You can share your role with the ansible galaxy community & also use the existing roles from the ansible galaxy community.

Search for a role with the below command,
```
ansible-galaxy search mysql
```

To use a role, 
```
ansible-galaxy install geerlingguy.mysql
```	
This role will be extracted to the default roles directory.
	
The roles can be used in your playbook ,
```
	-
		name: Install and Configure MySQL
		hosts: db_server
		roles:
		   - geerlingguy.mysql
```	   

To list the existing roles,
```
ansible-galaxy list
```
