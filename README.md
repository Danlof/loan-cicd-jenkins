## Jenkins CICD
- I will be using jenkins to keep track of the the development process of the loan app.
- These are mostly the instructions to build:
    - docker and run it 
    - track the development using jenkins.
### Some commands used to run docker, locally.
```
docker build -t danlof/cicd:latest . #-->  This builds the docker image
docker push danlof/cicd:latest # pushes the images to the docker hub

docker run -d -it --name modelv1 -p 8005:8005 danlof/cicd:latest bash # creates a docker image on the port 8005

docker exec modelv1 python prediction_model/training_pipeline.py # excecutes the training pipeline on that containeer 

docker exec modelv1 pytest -v --junitxml TestResults.xml --cache-clear # ensure good quality of code 

docker cp modelv1:/code/src/TestResults.xml . 

docker exec -d -w /code modelv1 python main.py # execute the 
```

## using Jenkins 
- Got to the official documentations of jenkins on how to install it together with java.

- This adds jenkins to the docker group  and adds current user to the docker group to be able to excute docker commands without `sudo` respectively
`sudo usermod -a -G docker jenkins
sudo usermod -a -G docker $USER
`

- Make sure to restart the EC2 instance for the changes to take effect.

### Enabling jenkins 
`sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins

`
#### Pasword for jenkins 
- For the password: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`

- Next install docker (instructions on the official website of linux docker installation)
- These 2 commands enable permissions on jenkins
`sudo usermod -a -G docker jenkins
sudo usermod -a -G docker $USER
`
### Setup Github repository for tracking changes
- Create a repo
- push data to github repo
- Generate personal access tokens and store in jenkins 
- setting up webhooks 