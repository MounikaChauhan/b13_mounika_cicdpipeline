
#clone the given repo link for the assignment submission

![alt text](images/image.png)

#For the Jekins assignment, I am Jenkins installed on a local vm

![alt text](images/image-1.png)

![alt text](images/image-2.png)

as, we are going to build python app, install the required libraries on the machine.

once the Jenkins is ready.

First we will run the app in local to test whether our application is running.

To run the application we need DB to be created which is in MongoDB.

Once the DB is created, get the connection string and upload in the .env file
after saving the file, run the application using the command provided.

Below screenshot shows the DB created and values provided.

![alt text](images/image-3.png)

![alt text](images/image-4.png)

let's create a pipeline for the same in Jenkins with automated test.

1. As we are using the env variable values we need to first declared them globally such that script can be used for fetching 

2. Run the pipeline by updating the script present in Jenkinsfile

![alt text](images/image-5.png)

This script consists for steps :
a. declare the environment variables
b. checking out to the code 
b. build the application using the commands
d. perform the pytest
e. send a mail for each build run

Initially my script has failed with error module not found, I have installed modules manually on the target machine 
![alt text](images/image-6.png)
![alt text](images/image-7.png)



