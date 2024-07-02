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
