# DevOps Project: CI/CD Pipeline with Jenkins, SonarQube, and Docker

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

- Set up **3 EC2 instances**:
  - **Jenkins server** (for CI/CD)
  - **SonarQube server** (for code quality analysis)
  - **Application Docker server** (for containerization)

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

