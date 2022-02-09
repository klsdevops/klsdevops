Create new branch from existing branch:

1.	CREATE A REMOTE REPOSITORY
			GO TO GITHUB & CREATE A NEW REPOSITORY "branch-testing-repo" FOR TESTING THE BRANCHING ACTIVITIES.
			ADD A README FILE WHILE CREATING THIS REPO.

![image](https://user-images.githubusercontent.com/90503660/153120253-ef3458d4-ebeb-43ef-812c-d0898d6178a7.png)

  2. CLONE THE REMOTE REPO TO YOUR LOCAL

     ```
     git clone https://github.com/klsdevops/branch-testing-repo.git
     ```
     
     ![image](https://user-images.githubusercontent.com/90503660/153120415-eb0da281-e683-4ecf-94d3-d257688e1761.png)

  3. VERIFY THE FILES IN THE DEFAULT "master" BRANCH & THE GIT LOG

     ![image](https://user-images.githubusercontent.com/90503660/153120584-4b19dd55-acfc-4c10-8949-911cc4c307c0.png)

  4. VERIFY THE EXISTING BRANCH DETAILS & CREATE A NEW BRANCH REFERENCING TO THE DEFAULT "master" BRANCH

     ![image](https://user-images.githubusercontent.com/90503660/153120967-9f537caf-7dae-4a36-afab-7765e76bfcd2.png)

  5. SWITCH TO THE NEW "feature" BRANCH AND VERIFY THE FILES & HISTORY DETAILS

     ![image](https://user-images.githubusercontent.com/90503660/153121194-021f59cb-f575-406b-8d14-6cf3cc7403ca.png)

     YOU COULD SEE ALL THE FILES AVAILABLE IN THE "master" REFERENCE BRANCH ARE AVAILABLE IN THE NEW "feature" BRANCH AS WELL.
     
  6. CREATE A NEW FILE IN THE FEATURE BRANCH & COMMIT IT TO THE REPOSITORY

     ![image](https://user-images.githubusercontent.com/90503660/153121687-d51d0ad1-3314-45fd-9363-79fbdabdd82c.png)

  7. SWITCH TO THE "master" BRANCH AND VERIFY THE DIFFERENCES

     ![image](https://user-images.githubusercontent.com/90503660/153121893-e199ed5c-9560-48c3-9954-d48024e86ed0.png)
     
     HERE YOU CAN NOT SEE THE CHANGES YOU HAVE MADE IN YOUR INDEPENDENT "feature" BRANCH.
     

    

     
