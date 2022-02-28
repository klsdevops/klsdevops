# To create a project template for webapp with maven

```
mvn archetype:generate -DgroupId=com.example -DartifactId=maven-project -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMod=false
```
# To create a project template for a sample Maven project.

```
mvn archetype:generate -DgroupId=com.klsdevops.project -DartifactId=simple-maven-project -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMod=false
```

# What is Archetype?

* Archetype is a Maven project templating toolkit. 
* Archetype will help authors create Maven project templates for users, and provides users with the means to generate parameterized versions of those project templates. 
* Using archetypes provides a great way to enable developers quickly in a way consistent with best practices employed by your project or organization.
 
- archetype:generate - Generates a new project from an archetype, or updates the actual project if using a partial archetype.
- interactiveMode - User settings used to check the interactiveMode.
- archetypeArtifactId - The archetype's artifactId.
- archetypeGroupId	- The archetype's groupId.
- groupId: Uniquely identifies your project across all projects.
- artifactId: is the name of the jar without version.
- pom.xml is the heart of a maven project where you maintain all the project related information.
  
# You issue the maven command with right archetype to create a project template

```
mvn archetype:generate -DgroupId=com.example -DartifactId=maven-project -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMod=false
```

![image](https://user-images.githubusercontent.com/90503660/155457579-c5f624bf-e0b8-4c66-85c6-9a34490e3efa.png)

![image](https://user-images.githubusercontent.com/90503660/155457652-5c146953-c4cd-4a40-aa05-5a6f4b8a107b.png)

# It has created a project structure

![image](https://user-images.githubusercontent.com/90503660/155457844-36dc4deb-f230-4f59-8dff-1d6ebafe6265.png)

# You could try packaging the application

```
mvn clean package
```

![image](https://user-images.githubusercontent.com/90503660/155461773-861f440f-bd94-44ff-a355-3faf1666bfb1.png)

# You could see a target folder has been created & the artifact file(.war) is generated there

![image](https://user-images.githubusercontent.com/90503660/155461847-7cc00e64-9b27-4fde-aab0-66cb21ea80f1.png)


