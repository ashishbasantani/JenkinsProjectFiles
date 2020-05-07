# JenkinsProjectFiles

## Flow Diagram
![flow3](https://user-images.githubusercontent.com/28612824/81254658-646b7e00-9049-11ea-8588-dbd60d8b5c58.jpg)

## Explaination of flow
1. The developer adds a new feature to the application either in the Master branch or Developer branch
2. After he feels everything is working fine so he commits the new feature
3. Git pushes the changes automatically to GitHub using post-commit hook and it pushes the feature to Master branch
4. As the new commit is being done in the Master branch Jenkins who always keep eye on it, download this new feature and put it into its workspace
5. The new feature which was put into the workspace is now copied to the production environment directory and a Docker container is launched (if it was not running already) which has the webserver for a production environment. Now the client can access this new feature
6. When developer commits in Developer branch Git automatically pushes the new feature into Developer branch of GitHub repository
7. As the new commit is being done in the Developer branch Jenkins who always keep eye on it, download this new feature and put it into its workspace
8. The new feature which was put into the workspace is now copied to the testing environment and a Docker container is launched (if it was not running already) which has the webserver for a testing environment. Now the QAT team can test the new feature.
9. QAT team now thoroughly test the new feature added by the developer
10. If everything looks fine with the new feature QAT provides a green flag and execute a python script which will execute job 3
11. Jenkins runs a job to merge the Master branch with the Developer branch so that the new feature can be added to the production environment. Congrats! now the client can access the new feature.

# Git repo creation and configuration
1. Create a repo which will already contain the Master branch
2. Now create another branch named Developer branch using ***"git branch Developer"*** command
3. Configure the Git hook so that whenver the commit is done it automatically pushes the changes to GitHub. 
![git](https://user-images.githubusercontent.com/28612824/81255225-c5e01c80-904a-11ea-845a-80af63a4af4b.png)

# Configuration of Jobs
## Job 1 (Eye on Master branch)
This job is for keeping track of the master branch of Git Hub. This job continuously keeps track of the commits done and whenever a new commit is done by the developer this job automatically downloads the data from Git Hub and copies it to the webserver environment folder. This job also launches the Docker container (if it was not running already) in which the production environment is running. This job helps to achieve the task of automatically putting new features into production.

### Screenshots of configuration

![job 1a](https://user-images.githubusercontent.com/28612824/81255502-69c9c800-904b-11ea-961e-2d31184a5fb8.png)
![job 1b](https://user-images.githubusercontent.com/28612824/81255504-6afaf500-904b-11ea-8f60-b330e40d6f83.png)
![job 1c](https://user-images.githubusercontent.com/28612824/81255507-6c2c2200-904b-11ea-8592-b8eb0472c883.png)

## Job 2 (Eye on Developer branch)

![job 2a](https://user-images.githubusercontent.com/28612824/81255492-62a2ba00-904b-11ea-9482-db7a64494dba.png)
![job 2b](https://user-images.githubusercontent.com/28612824/81255495-66364100-904b-11ea-8cf4-23e8390c171d.png)

## Job 3 (Merge branches to integrate new features)

![job 3a](https://user-images.githubusercontent.com/28612824/81255497-67676e00-904b-11ea-936f-2d98d3c94b13.png)
![job 3b](https://user-images.githubusercontent.com/28612824/81255499-68989b00-904b-11ea-9f31-23685909ba4d.png)
![job 3c](https://user-images.githubusercontent.com/28612824/81255501-69313180-904b-11ea-81f3-1d9dc5e42721.png)
