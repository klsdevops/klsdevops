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
  Both _Declarative_ and _Scripted Pipeline_ are DSLs to describe portions of your software delivery pipeline. Scripted Pipeline is written in a limited form of _Groovy syntax_.
  A Pipeline can be created through the _Classic UI_ method or _In SCM_ write a _Jenkinsfile_ manually, which you can commit to your project’s source control repository. 
  
  
