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

- click on create a job, enter the item name, click on freestyle and then on.
- in the general -> GitHub project -> Project url <enter gihub repo url> 
