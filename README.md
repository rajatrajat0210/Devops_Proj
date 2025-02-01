# DevOps Project: CI/CD Pipeline with Jenkins, SonarQube, and Docker

![image alt](https://github.com/rajatrajat0210/Devops_Proj/blob/master/CI:CD-Pipeline.jpg?raw=true)


This project demonstrates a DevOps pipeline setup using **AWS EC2 instances** (virtual machines), **Jenkins** for Continuous Integration/Continuous Deployment (CI/CD), **SonarQube** for code quality checks, and **Docker** for containerization. The entire setup is designed to automatically integrate code from **GitHub**, run quality checks, and deploy the application in containers.

---

## 🚀 Project Overview

This project sets up a robust pipeline with the following components:

- **Jenkins**: Automates the build, test, and deployment process.
- **SonarQube**: Analyzes code quality and integrates with Jenkins to ensure best practices.
- **Docker**: Packages the application into containers for easy deployment across different environments.
- **AWS EC2 Instances**: Hosts the servers for Jenkins, SonarQube, and the application.

---

## 🔧 Prerequisites

Before you begin, make sure you have the following:

- An **AWS account** and EC2 instances set up.
- A **GitHub** account with a repository for your project.
- **Jenkins** installed on one EC2 instance.
- **SonarQube** installed on a separate EC2 instance.
- **Docker** installed on another EC2 instance for containerization.

---

## ⚙️ Setup Guide

### 1. **AWS EC2 Instances**

![image alt](https://github.com/rajatrajat0210/Devops_Proj/blob/master/AWS_EC2.jpg?raw=true)

- Set up **3 EC2 instances**:
  - **Jenkins server** (for CI/CD)
  - **SonarQube server** (for code quality analysis)
  - **Application Docker server** (for containerization)

![image alt](https://github.com/rajatrajat0210/Devops_Proj/blob/master/VM's_servers.jpg?raw=true)


### 2. **Jenkins Setup**

- **Install Jenkins** on the EC2 instance:

  ```bash
  sudo apt update
  sudo apt install openjdk-11-jdk
  wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee /etc/apt/trusted.gpg.d/jenkins.asc
  sudo sh -c 'echo deb http://pkg.jenkins.io/debian/jenkins.io.stable/ / > /etc/apt/sources.list.d/jenkins.list'
  sudo apt update
  sudo apt install jenkins
  sudo systemctl start jenkins
  sudo systemctl enable jenkins

  ### Access Jenkins through http://<your-jenkins-server-ip>:8080 and complete the setup wizard.
3. GitHub Integration with Jenkins
Install the GitHub plugin on Jenkins:
Go to Manage Jenkins > Manage Plugins > Available and search for the GitHub plugin. Install it.
Create a GitHub webhook to trigger Jenkins builds automatically whenever code is pushed:
Go to GitHub > Settings > Webhooks > Add webhook, and set the Payload URL to http://<your-jenkins-server-ip>:8080/github-webhook/.
4. SonarQube Setup
Install SonarQube on the EC2 instance:

```bash
Copy
Edit
sudo apt install openjdk-11-jdk
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.0.0.45655.zip
unzip sonarqube-9.0.0.45655.zip
sudo mv sonarqube-9.0.0.45655 /opt/sonarqube
cd /opt/sonarqube/bin/linux-x86-64
./sonar.sh start
Access SonarQube at http://<your-sonarqube-server-ip>:9000. 

```
Default SonarQube login:

Username: admin
Password: admin
5. SonarQube Integration with Jenkins
Install the SonarQube plugin in Jenkins:

Go to Manage Jenkins > Manage Plugins > Available and search for the SonarQube plugin. Install it.
Configure Jenkins to use SonarQube for code analysis:

Go to Manage Jenkins > Configure System.
Under SonarQube servers, add the SonarQube server URL (e.g., http://<your-sonarqube-server-ip>:9000).
Add authentication credentials if needed.
Create a Jenkins job to run SonarQube analysis:

In the Jenkins job configuration, add a SonarQube Scanner build step:
Execute SonarQube Scanner to analyze the code.
6. Docker Setup
Install Docker on the Docker server EC2 instance:

```bash
Copy
Edit
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/trusted.gpg.d/docker.asc
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce
sudo systemctl start docker
sudo systemctl enable docker
```
###Create a Dockerfile for your application:

Example Dockerfile:

Dockerfile
Copy
Edit
FROM openjdk:11-jdk
COPY . /app
WORKDIR /app
RUN javac MyApp.java
CMD ["java", "MyApp"]
Build and run your Docker image:

```bash
Copy
Edit
docker build -t myapp .
docker run -d -p 8080:8080 myapp
Push the Docker image to Docker Hub or AWS ECR:
```
For Docker Hub:

```bash
Copy
Edit
docker login
docker tag myapp <your-dockerhub-username>/myapp
docker push <your-dockerhub-username>/myapp
🛠️ How the Pipeline Works
Push Code to GitHub:
```
Developers push code to the GitHub repository.
Jenkins Triggers Build:

![image alt](https://github.com/rajatrajat0210/Devops_Proj/blob/master/jenkins_build.jpg?raw=true)


Jenkins detects the code change via GitHub Webhook.
Jenkins pulls the latest code from GitHub and triggers the build.
SonarQube Code Analysis:

Jenkins invokes SonarQube to analyze the code for quality issues.
If the code passes the quality checks, Jenkins proceeds with the build; otherwise, it notifies the developer.
Build and Containerize with Docker:

Jenkins creates a Docker image from the application code.
The image is pushed to Docker Hub or AWS ECR.
Deploy the Docker Container:

The Docker container is deployed to the Docker EC2 instance for testing or production.


## 📜 Conclusion
This project integrates Jenkins for automating the CI/CD pipeline, SonarQube for continuous code quality checks, and Docker for containerizing applications. The entire pipeline is hosted on AWS EC2 instances, ensuring scalability and reliability.

## 💬 Contribution
Feel free to contribute to this project by raising issues, submitting pull requests, or suggesting improvements. 😊

