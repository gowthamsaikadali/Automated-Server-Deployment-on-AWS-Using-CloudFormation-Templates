# 🚀 Automated Server Deployment on AWS Using CloudFormation Templates

## 📌 Project Overview

This project demonstrates **Infrastructure as Code (IaC)** by automating the deployment of a web server on **Amazon Web Services (AWS)** using **AWS CloudFormation**. The solution provisions the required cloud infrastructure, configures an EC2 instance with **Nginx**, and deploys a static website hosted from files stored in an **Amazon S3** bucket.

The primary goal is to eliminate manual infrastructure provisioning and server configuration by using reusable CloudFormation templates.

---

## 🎯 Objectives

* Automate AWS infrastructure deployment using CloudFormation.
* Create an Amazon S3 bucket for hosting website assets.
* Upload static website files (HTML, CSS, JavaScript) to S3.
* Provision networking resources such as VPC, Subnet, Internet Gateway, Route Table, and Security Group.
* Launch an EC2 instance with a public IP address.
* Automatically install and configure Nginx using EC2 User Data.
* Deploy the website by replacing the default Nginx page with files from the S3 bucket.
* Verify successful deployment by accessing the application through the EC2 public IP.

---

## 🏗️ Architecture

```text
                  +---------------------------+
                  |      Website Source       |
                  | (HTML, CSS, JavaScript)   |
                  +------------+--------------+
                               |
                               v
                    +----------------------+
                    |     Amazon S3 Bucket |
                    |  Static Website Files|
                    +-----------+----------+
                                |
                                |
                    CloudFormation Templates
                                |
                                v
          +-------------------------------------------+
          |         AWS CloudFormation Stack           |
          +-------------------+------------------------+
                              |
          -----------------------------------------------------
          |                    |                            |
          v                    v                            v
     Amazon VPC          Security Group             Internet Gateway
          |                    |                            |
          ---------------------+----------------------------
                               |
                               v
                      Public Subnet & Route Table
                               |
                               v
                    +--------------------------+
                    |      EC2 Instance         |
                    |   Ubuntu + Nginx Server   |
                    +-------------+-------------+
                                  |
                 User Data installs Nginx and copies
                 website files from Amazon S3
                                  |
                                  v
                      Static Website Hosted on Nginx
                                  |
                                  v
                    Access via EC2 Public IPv4 Address
```

---

## 🛠️ Technologies Used

* AWS CloudFormation
* Amazon EC2
* Amazon S3
* Amazon VPC
* Internet Gateway
* Route Tables
* Security Groups
* Ubuntu Linux
* Nginx Web Server
* HTML5
* CSS3
* JavaScript
* YAML

---

## 📂 Repository Structure

```text
├── README.md
├── index.html
├── style.css
├── script.js
├── s3-CloudFormation-Template.yaml
└── webserver.yaml
```

---

## 📋 Deployment Steps

### Step 1: Create the Amazon S3 Bucket

* Deploy the `s3-CloudFormation-Template.yaml` template.
* Create an S3 bucket for storing website assets.
* Configure the bucket with appropriate public access settings and bucket policy.

### Step 2: Upload Website Files

Upload the following files to the S3 bucket:

* `index.html`
* `style.css`
* `script.js`
* Images and other static assets (if applicable)

### Step 3: Deploy the Infrastructure

Deploy the `webserver.yaml` CloudFormation template.

The template provisions:

* VPC
* Public Subnet
* Internet Gateway
* Route Table
* Security Group
* EC2 Instance
* Public IP assignment

### Step 4: Automatic Server Configuration

During instance launch, the EC2 User Data script:

* Updates system packages
* Installs Nginx
* Retrieves website files from Amazon S3
* Replaces the default Nginx web content
* Starts and enables the Nginx service

### Step 5: Verify Deployment

After the CloudFormation stack completes successfully:

1. Open the EC2 console.
2. Copy the Public IPv4 Address of the instance.
3. Paste it into a web browser.
4. The deployed static website should be displayed.

---

## 📸 Suggested Screenshots

Include screenshots for:

* S3 bucket creation
* Bucket policy configuration
* Website file upload
* CloudFormation stack creation
* EC2 instance details
* Security group configuration
* Successful stack completion
* Website accessed using the EC2 public IP

---

## ✅ Project Outcome

The project successfully automates the deployment of a web server and static website using AWS CloudFormation. By combining Amazon S3 for asset storage with EC2 User Data and Nginx configuration, the solution demonstrates a repeatable and efficient Infrastructure as Code workflow.

---

## 🌟 Key Features

* Infrastructure as Code (IaC)
* Automated AWS resource provisioning
* Nginx installation without manual intervention
* Static website deployment from Amazon S3
* Publicly accessible web server
* Reusable CloudFormation templates
* Minimal manual configuration

---

## 📚 Learning Outcomes

Through this project, you will gain practical experience with:

* AWS CloudFormation
* Infrastructure as Code principles
* Amazon EC2 provisioning
* Amazon S3 object storage
* Nginx web server configuration
* Cloud automation workflows
* Static website hosting on AWS

---

## 👨‍💻 Author

**Gowtham Sai Kadali**
**Role:** Multi-Cloud & DevSecOps Engineer

If you found this project useful, consider giving the repository a ⭐ on GitHub.
