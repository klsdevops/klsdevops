# Register with Azure DevOps & Create a backlog with the below items & add it to corresponding sprints
https://dev.azure.com/

1. Register with Azure DevOps https://dev.azure.com/
2. Create backlog for the below; Make sure that all the required details are captured in the description area & the Acceptance Criteria is well written.
    * Create a new GITHUB Project (Maven based Java Project)
    * Define your branching strategy. You could just write how your code flow should happen in the Description area of the User Story.
    * Create other default branches (Develop, Release etc.).
    * Setup the security settings to protect the default branches, so that no one can push the code directly to the default branches.
        - Make sure that even Administratory can not do direct push to default branches
        - Make sure that all conversation should be resolved before merging
        - Make sure that require minimum one approvals for merging.
    * Clone the Remote Repository & perform code updates on index.jsp page and the updates should be available on the Remote Develop branch.
    * Setup Jenkins Server
    * Create a build pipeline for the application.
    * Setup the application servers (Dev & Release environments)
    * Perform a deployment to the Dev environment
    * Automate the complete CICD with Jenkins file & the deployment should happen to the respective environments w.r.t code updates/merge strategy.
   
