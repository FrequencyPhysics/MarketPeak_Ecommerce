
# Capstone Project: E-Commerce Platform Deployment with Git, Linux, and AWS

## Project Overview
This project involves the development and deployment of an e-commerce website for a new online marketplace called “MarketPeak.” The platform will feature product listings, a shopping cart, and user authentication, among other functionalities.

## Table of Contents
1. [Implement Version Control with Git](#1-implement-version-control-with-git)
2. [AWS Deployment](#2-aws-deployment)
3. [Continuous Integration and Deployment Workflow](#3-continuous-integration-and-deployment-workflow)
4. [Challenges Faced](#4-challenges-faced)
5. [Conclusion](#5-conclusion)

## 1. Implement Version Control with Git

### 1.1 Initialize Git Repository
- Created a project directory named `MarketPeak_Ecommerce`:
  ```bash
  mkdir MarketPeak_Ecommerce
  ```
- Initialized a Git repository to manage version control:
  ```bash
  cd MarketPeak_Ecommerce
  git init
  ```

### 1.2 Obtain and Prepare the E-commerce Website Template
- Downloaded a suitable e-commerce website template from Tooplate.
- Extracted the downloaded template into the project directory `MarketPeak_Ecommerce`.

### 1.3 Stage and Commit the Template to Git
- Added website files to the Git repository:
  ```bash
  git add .
  ```
- Configured Git with my email and username:
  ```bash
  git config --global user.name "FrequencyPhysics"
  git config --global user.email "ademide.ajiboye@gmail.com"
  ```
- Committed the changes with a descriptive message:
  ```bash
  git commit -m "Initial commit with basic e-commerce site structure"
  ```

### 1.4 Push the Code to GitHub
- Logged into my GitHub account and created a new repository named `MarketPeak_Ecommerce`.
- Linked the local repository to GitHub:
  ```bash
  git remote add origin https://github.com/FrequencyPhysics/MarketPeak_Ecommerce.git
  ```
- Pushed the code to GitHub:
  ```bash
  git push -u origin master
  ```

## 2. AWS Deployment

### 2.1 Setting Up an AWS EC2 Instance
- Logged into the AWS Management Console.
- Launched an EC2 instance using an Amazon Linux AMI.
- Connected to the instance using SSH:
  ```bash
  ssh -i "ecom.pem" ec2-user@3.88.87.47
  ```

### 2.2 Clone the Repository on the Linux Server

#### SSH Method:
- Generated an SSH key pair on the EC2 instance:
  ```bash
  ssh-keygen
  ```
- Displayed and copied the public key:
  ```bash
  cat /home/ec2-user/.ssh/id_rsa.pub
  ```
- Added the SSH public key to my GitHub account.
- Used the SSH clone URL to clone the repository:
  ```bash
  git clone git@github.com:FrequencyPhysics/MarketPeak_Ecommerce.git
  ```

#### HTTPS Method:
- Alternatively, used the HTTPS clone URL:
  ```bash
  git clone https://github.com/FrequencyPhysics/MarketPeak_Ecommerce.git
  ```

### 2.3 Install a Web Server on EC2
- Installed Apache HTTP server (httpd) on the EC2 instance:
  ```bash
  sudo yum update -y
  sudo yum install httpd -y
  sudo systemctl start httpd
  sudo systemctl enable httpd
  ```

### 2.4 Configure `httpd` for Website
- Cleared the default `httpd` web directory:
  ```bash
  sudo rm -rf /var/www/html/*
  ```
- Copied the MarketPeak Ecommerce website files to the web directory:
  ```bash
  sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/
  ```
- Reloaded `httpd` to apply the changes:
  ```bash
  sudo systemctl reload httpd
  ```

### 2.5 Access Website from Browser
- Edited the "Inbound rules" in the AWS console EC2 instance settings:
  - Set the Inbound rules to "HTTP," Port range – 80, Source 0.0.0.0/0.
- Accessed the EC2 instance's public IP address in a web browser:
  ```bash
  http://3.88.87.47/2130_waso_strategy/
  ```

## 3. Continuous Integration and Deployment Workflow

### 3.1 Developing New Features and Fixes
- Created a development branch for new features and fixes:
  ```bash
  git branch development
  ```
- Switched to the development branch:
  ```bash
  git checkout development
  ```

### 3.2 Version Control with Git
- Added new changes to Git:
  ```bash
  git add .
  ```
- Committed the changes:
  ```bash
  git commit -m "Added new features and fix bugs"
  ```
- Pushed the changes to GitHub:
  ```bash
  git push origin development
  ```

### 3.3 Created Pull Request and Merged to Main Branch
- Created a Pull Request (PR) on GitHub.
- Reviewed and merged the PR.
- Switched to the main branch:
  ```bash
  git checkout main
  ```
- Merged the development branch into the main branch:
  ```bash
  git merge development
  ```

### 3.4 Deploying Updates to the Production Server
- Pulled the latest changes on the server:
  - Logged into the AWS EC2 instance using SSH and navigated to the website directory:
    ```bash
    ssh -i "ecom.pem" ec2-user@3.88.87.47
    cd MarketPeak_Ecommerce
    git pull origin main
    ```
- Restarted the web server to apply the changes:
  ```bash
  sudo systemctl reload httpd
  ```

### 3.5 Testing the New Changes
- Accessed the website by opening a web browser and navigating to the public IP address of the EC2 instance:
  ```bash
  http://3.88.87.47/2130_waso_strategy/
  ```
- Verified that the new features are working as expected.

## 4. Challenges Faced
During the deployment process, one significant challenge arose when I attempted to access the public IP address of my EC2 instance in a web browser. Despite following all the necessary steps to configure the Apache server and set up the website files, the site did not load as expected. This issue persisted, leading to frustration as I repeatedly checked my configurations, security group settings, and Apache server status.

After some investigation and seeking help from peers and online forums, I discovered that the problem was related to the EC2 instance's security group settings. I had mistakenly modified the inbound rules to allow only HTTP traffic by deleting the SSH rule, which inadvertently blocked my ability to access the instance via the terminal. With guidance, I re-added the SSH rule and ensured that both HTTP and SSH traffic were properly configured in the security group. Additionally, I checked that the Apache server was running correctly and that the website files were properly placed in the `/var/www/html/` directory.

This collaborative troubleshooting experience was invaluable in overcoming the issue and successfully deploying the website. It also highlighted the importance of careful configuration and the willingness to seek assistance when facing roadblocks.

## 5. Conclusion
This capstone project provided a comprehensive learning experience in deploying an e-commerce platform using Git, Linux, and AWS. Throughout the process, I gained hands-on experience with version control, server management, and continuous integration workflows. The challenges I encountered, particularly with accessing the server's IP address, emphasized the importance of troubleshooting skills and collaboration.

Successfully deploying the MarketPeak e-commerce platform was a significant achievement, as it involved not only technical knowledge but also problem-solving and teamwork. The final result is a functional website that can be accessed and managed remotely, laying a strong foundation for future enhancements and scaling. This project has solidified my understanding of cloud-based deployments and prepared me for more advanced projects in the future.
```
