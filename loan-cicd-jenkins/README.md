## Jenkins CICD
- I will be using jenkins to keep track of the the development process of the loan app.
- These are mostly the instructions to build:
    - docker and run it 
    - track the development using jenkins.
    - An EC2 instance will be in use, everything is run on cloud.

## Installing and using jenkins 
- Go to the official documentations of jenkins on how to install it together with java.
- Run this command to enable and check if it is working:
```
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```
#### Pasword for jenkins 
- For the password: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`

### Install docker 
Go to to the official documentation of docker and install it as per the instructions:
-The following adds jenkins to the docker group  and adds current user to the docker group to be able to excute docker commands without `sudo` respectively
```
sudo usermod -a -G docker jenkins
sudo usermod -a -G docker $USER
```

- Make sure to restart the EC2 instance for the changes to take effect.

- Next install docker (instructions on the official website of linux docker installation)

### Some commands used to run docker.
```
docker build -t danlof/cicd:v1 . 
docker push danlof/cicd:v1

docker run -d -it --name loanv1 -p 8005:8005 danlof/cicd:v1 bash

docker exec loanv1 python prediction_model/training_pipeline.py

docker exec loanv1 pytest -v --junitxml TestResults.xml --cache-clear

docker cp loanv1:/code/src/TestResults.xml .

docker exec -d -w /code loanv1 python main.py
```
 
### EC2 instance 
- Make sure to use and instance with enough space to avoid issues with the run and build of the docker images and containers. i.e t2 medium is okay
 

