# Declarative Pipeline
Declarative Pipeline is a relatively recent addition to Jenkins Pipeline which presents a more simplified and opinionated syntax on top of the Pipeline sub-systems.

All valid Declarative Pipelines must be enclosed within a pipeline block, for example:

```
pipeline {
    /* insert Declarative Pipeline here */
}
```

The most fundamental part of a Pipeline is the "step". Basically, steps tell Jenkins what to do and serve as the basic building block for both Declarative and Scripted Pipeline syntax.

Declarative Pipeline follow the below rules,

  * The top-level of the Pipeline must be a block, specifically: _pipeline { }_.
  * No semicolons as statement separators. Each statement has to be on its own line.
  * Blocks must only consist of _Sections_, _Directives_, _Steps_, or assignment statements.
  * A property reference statement is treated as a no-argument method invocation. So, for example, _input_ is treated as _input()_.

For writing the Declarative Pipeline Syntax, you can get help from the Declarative Generator which is basically _<YOUR JENKINS URL>/declarative-generator_
  
 Eg; http://3.22.222.129:8080/directive-generator/
  
  Select the desired directive in the dropdown menu
  Use the dynamically populated area below the dropdown to configure the selected directive.
  Click Generate Directive to create the directive’s configuration to copy into your Pipeline.
  
## Using a Jenkinsfile
  Complex Pipelines are difficult to write and maintain within the classic UI’s Script text area of the Pipeline configuration page.
  To make this easier, your Pipeline’s **_Jenkinsfile_** can be written in a text editor or integrated development environment (IDE) and committed to source control.
  Jenkins can then check out your **_Jenkinsfile_** from source control as part of your Pipeline project’s build process and then proceed to execute your Pipeline.
  
  ### Getting started with Pipeline
  **Prerequisites**
    * Jenkins 2.x or later (older versions back to 1.642.3 may work but are not recommended)
    * Pipeline plugin, which is installed as part of the "suggested plugins"
  
  **Defining a Pipeline**
  Both _Declarative_ and _Scripted Pipeline_ are DSLs(Domain Specific Language) to describe portions of your software delivery pipeline. Scripted Pipeline is written in a limited form of _Groovy syntax_.
  A Pipeline can be created through the _Classic UI_ method or _In SCM_ write a _Jenkinsfile_ manually, which you can commit to your project’s source control repository. 
  
  ### Through Classic UI
  #### Select "new item" and select the "Pipeline" from options and click "OK"  
  ![image](https://user-images.githubusercontent.com/90503660/136320569-c5d7518d-a50f-4886-8069-5b3b71b727b5.png)
  
  #### Go to the "Pipeline" tab and write your Pipeline code into the Script text area
  Copy the following Declarative example Pipeline code and paste this into the Script text area. 
    
```
pipeline {
    agent any 
    stages {
        stage('Stage 1') {
            steps {
                echo 'Hello world!' 
            }
        }
    }
}
```

![image](https://user-images.githubusercontent.com/90503660/136320696-eed5f58a-3b8e-48a1-9b40-e88731acfecc.png)

* _agent_ instructs Jenkins to allocate an executor (on any available agent/node in the Jenkins environment) and workspace for the entire Pipeline.
* _echo_ writes simple string in the console output.
* _node_ effectively does the same as _agent_ (above).

**NOTE:** You can even try the "try sample Pipeline" option at the top right of the Script text area. 

#### Click Apply & Save to open the Pipeline project/item view page.
#### Now, run the pipeline to see the results (Click "Build Now")

![image](https://user-images.githubusercontent.com/90503660/136321200-2841bf38-808d-4ab7-a8d8-04128df74beb.png)

#### When you click on the stage logs, you can see the script output

![image](https://user-images.githubusercontent.com/90503660/136321274-3d4b1524-6d8e-433d-a7a3-89f5243b5528.png)

#### Under Build History on the left, click #1 to access the details for this particular Pipeline run.
#### Click Console Output to see the full output from the Pipeline run. The following output shows a successful run of your Pipeline.

![image](https://user-images.githubusercontent.com/90503660/136321398-5fb14200-48e9-4b91-b3d8-f2cb71c0f0d4.png)

**NOTE:** Defining a Pipeline through the classic UI is convenient for testing Pipeline code snippets, or for handling simple Pipelines or Pipelines that do not require 
          source code to be checked out/cloned from a repository.
          Jenkinsfiles entered into the Script text area of Pipeline projects are stored by Jenkins itself, within the Jenkins home directory.
          For greater control and flexibility over your Pipeline, it is recommended that you use _source control_ to define your _Jenkinsfile_.


    
