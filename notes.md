### To Run a Spring boot application

### Architecture of the project
![preview](./Images/j0.png)

### Install Jenkins

* to run jenkins we require java
* install jenkins and java [Refer Here](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu) or run the belus script
```
#!/bin/bash
sudo apt update
sudo apt install openjdk-17-jdk -y
### jenkins installation
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
```
* To open jenkins `http://<ip address>:8080`
![preview](./Images/j1.png)
* To get the Admin password
![preview](./Images/j2.png)
![preview](./Images/j3.png)
![preview](./Images/j4.png)
![preview](./Images/j5.png)
![preview](./Images/j6.png)

* Now install Docker plugin to run the jenkinsfile inside docker , Now docker will be an agent.
![preview](./Images/j7.png)
![preview](./Images/j8.png)
![preview](./Images/j9.png)

* now install sonar plugin
![preview](./Images/j10.png)

### create a new ec2 instance and configure a Sonar Server locally
```
sudo apt update
sudo apt install openjdk-11-jdk
sudo apt install unzip -y
sudo adduser sonarqube
sudo su - sonarqube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.6.1.59531.zip
unzip sonarqube-9.6.1.59531.zip
chmod -R 755 /home/sonarqube/sonarqube-9.6.1.59531
chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.6.1.59531
cd sonarqube-9.6.1.59531/bin/linux-x86-64
./sonar.sh start
./sonar.sh status
```
* To open sonarqube `http://<ip address>:9000`
![preview](./Images/j11.png)

### configure sonarqube with jenkins
* Go to my account section in sonarqube
* Go to security and enter name for token and generate token
![preview](./Images/j12.png)
![preview](./Images/j13.png)
* Now in jenkins
![preview](./Images/j14.png)
![preview](./Images/j15.png)
* now here enter the key generated in sonarqube
![preview](./Images/j16.png)

### install docker
```
sudo apt update
sudo apt install docker.io
sudo usermod -aG docker ubuntu
sudo systemctl restart docker
```
* configure docker credentials in jenkins
![preview](./Images/j17.png)
* configure github credentials in jenkins
