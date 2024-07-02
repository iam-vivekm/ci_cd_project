# ci_cd_project
This is CI CD project using ec2, nodejs, docker, jenkins.

Step 1. 
launch an EC2 machine.

Step 2: Install Jenkins on EC2 Instance:
  - apt-get update
  - apt install openjdk-11-jre
  - java -version
  - curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
  - echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
- apt-get update -y
- apt-get install jenkins -y
- systemctl enable jenkins
- systemctl start jenkins
- systemctl status jenkins

Now run yourpublicip:8080 in the browser to check jenkins is install or not.
run the below command so you will get your jenkins password.

- cat /var/lib/jenkins/secrets/initialAdminPassword
  
after enter the password install suggested plugins.

Step 3. Build a project

- to build a job we have top create a ssh keygen so that git hub repo and server can communicate.
- on the server type ssh-keygen, it will give you two secret key. one is public and other one is private. We will use public key in github and private key in jenkins.
  - go to guthub and click on settings
  - click on SSH and GPG keys
  - click on new ssh key
  - enter the title and paste your public key here.
  - now go to jenkins and under general -> source code management -> git -> repository url <paste github repo url>
  - under credentials click on jenkins -> kind -> ssh username with private key -> ID(whatever you want to name it) -> username(server username) -> private key -> enter directly and paste your private key here.
  - click on add and save.

 - check all the setting is configured or not so click on build now.

Step 4. Run the code
- cd /var/lib/jenkins/workspace/project_name
- apt insatll nodejs -y
- apt install npm
- npm install
- node app.js
- now open the browser and copy yourpublicip:8080

  Step 5. if you want to run app using docker.
  - install docker
  - apt-get install docker.io
  - # build dockerfile
  - vi Docker file
FROM node
WORKDIR app
COPY . .
RUN npm install
EXPOSE 8000
CMD ["node","app.js"]
- docker build . -t image_name
- docker run -d --name container_name -p 8080:8080 image_name
  
now go to browser and use public_ip:8080

Step 6. use jenkins so that you don't have to run docker commands manually.
- click on configure
- Build Steps
- Execute shell
- docker build . -t image_name
- docker run -d --name cont_name -p 8000:8000 image_name
- now click on build now it will automatic create a container and run app.

 Step 7. CI CD
 - for ci cd you have to install github integration plugin in jenkins
 - after that go to setting of repo
 - go to webhook
 - add webhook
 - paste punlicip:8080/github-webhook/ under the payload url
 - under the jenkins
 - go to configure
 - under Build Triggers
 - click on GitHub hook trigger for GITScm polling
Now whenever a new code push in the repo then the pipeline automatically triggerd.
