# Automated Server Deployment using AWS CloudFormation

## 📌 Project Overview

This project demonstrates how to automate the deployment of a web server and static web application on AWS using **AWS CloudFormation (Infrastructure as Code)**.

The CloudFormation template provisions the required networking resources, launches an Ubuntu EC2 instance, installs and configures Nginx, and deploys a static website by replacing the default Nginx content with custom application files.

---

## 🚀 Features

* Infrastructure as Code using AWS CloudFormation
* Automated creation of a custom VPC
* Public subnet with Internet connectivity
* Internet Gateway and Route Table configuration
* Security Group with HTTP and SSH access
* Ubuntu EC2 instance deployment
* Automatic Nginx installation using UserData
* Automated deployment of static website files
* Publicly accessible web application using EC2 Public IP
* Reproducible and consistent infrastructure deployment

---

## 🏗️ Architecture

```text
                    AWS CloudFormation
                            │
                            ▼
                   Creates Networking Stack
                            │
          ┌─────────────────┴─────────────────┐
          │                                   │
          ▼                                   ▼
        VPC                           Internet Gateway
          │                                   │
          └──────────────┬────────────────────┘
                         │
                  Public Route Table
                         │
                         ▼
                   Public Subnet
                         │
                         ▼
                 Security Group (22, 80)
                         │
                         ▼
                 Ubuntu EC2 Instance
                         │
                 Cloud-Init / UserData
                         │
         ┌───────────────┼────────────────┐
         │               │                │
         ▼               ▼                ▼
   Install Nginx   Download Website   Configure Nginx
         │
         ▼
    /var/www/html
         │
         ▼
  Static Website Available
      via Public IP
```

---

## 🛠️ Technologies Used

* AWS CloudFormation
* Amazon EC2
* Amazon VPC
* Amazon S3
* Ubuntu Server
* Nginx
* YAML
* Bash (UserData)

---

## 📂 Project Structure

```text
.
├── webserver.yaml          # CloudFormation template
├── index.html              # Website homepage
├── style.css               # Stylesheet
├── script.js               # JavaScript logic
└── README.md               # Project documentation
```

---

## 📋 Prerequisites

Before deploying the project:

* AWS Account
* AWS Management Console access
* Existing EC2 Key Pair
* CloudFormation permissions
* S3 bucket containing:

  * `index.html`
  * `style.css`
  * `script.js`

---

## ⚙️ Deployment Steps

### Step 1: Upload Website Files

Create an Amazon S3 bucket and upload your website files:

```text
index.html
style.css
script.js
```

Ensure the EC2 instance can read these objects (either through public access or an IAM role with S3 read permissions).

---

### Step 2: Create CloudFormation Stack

1. Open AWS Console.
2. Navigate to **CloudFormation**.
3. Click **Create Stack**.
4. Select **Upload a template file**.
5. Upload `webserver.yaml`.
6. Click **Next**.

---

### Step 3: Configure Stack

Provide:

* Stack Name
* EC2 Key Pair
* Any template parameters (if applicable)

Then continue through the wizard and create the stack.

---

### Step 4: Automatic Provisioning

CloudFormation provisions:

* VPC
* Public Subnet
* Internet Gateway
* Route Table
* Security Group
* Ubuntu EC2 Instance

The EC2 UserData script then:

* Updates packages
* Installs Nginx
* Starts and enables the Nginx service
* Downloads website files
* Replaces the default Nginx content in `/var/www/html`
* Restarts Nginx

---

### Step 5: Access the Website

After the stack reaches `CREATE_COMPLETE`, retrieve the EC2 Public IP from the CloudFormation Outputs or EC2 Console.

Example:

```text
http://<EC2-PUBLIC-IP>
```

---

## 🔒 Security Group Configuration

| Port | Protocol | Purpose          |
| ---- | -------- | ---------------- |
| 22   | TCP      | SSH Access       |
| 80   | TCP      | HTTP Web Traffic |

---

## 📊 CloudFormation Resources

The template provisions:

* AWS::EC2::VPC
* AWS::EC2::Subnet
* AWS::EC2::InternetGateway
* AWS::EC2::RouteTable
* AWS::EC2::Route
* AWS::EC2::SubnetRouteTableAssociation
* AWS::EC2::SecurityGroup
* AWS::EC2::Instance

---

## 📁 Website Deployment Path

The application is deployed to:

```text
/var/www/html/
```

The default Nginx page is replaced with the custom website files.

---

## 🧪 Verification

Verify the deployment by:

* Confirming the CloudFormation stack status is `CREATE_COMPLETE`
* Ensuring the EC2 instance is in the `running` state
* Checking that Nginx is active:

  ```bash
  sudo systemctl status nginx
  ```
* Visiting:

  ```text
  http://<EC2-PUBLIC-IP>
  ```

---

## ⚠️ Troubleshooting

### 403 Forbidden

Possible causes:

* `index.html` is missing from `/var/www/html`
* Website files could not be downloaded from S3
* S3 permissions prevent object access

### UserData Logs

Inspect cloud-init logs:

```bash
sudo cat /var/log/cloud-init-output.log
```

### Verify Website Files

```bash
ls -la /var/www/html
```

Expected:

```text
index.html
style.css
script.js
```

---

## 📈 Future Enhancements

* IAM Role for secure S3 access instead of public objects
* Elastic IP for a static public address
* Application Load Balancer
* Auto Scaling Group
* HTTPS using ACM and Nginx
* CI/CD integration with GitHub Actions or AWS CodePipeline
* Parameterized CloudFormation template for reusable deployments

---

## 🎯 Learning Outcomes

By completing this project, you gain hands-on experience with:

* Infrastructure as Code (IaC)
* AWS CloudFormation
* EC2 provisioning
* VPC networking
* Security Groups
* Nginx configuration
* Automated server bootstrapping using UserData
* Static website deployment on AWS

---

## 👨‍💻 Author

**Kadali Gowtham Sai**
**Multi Cloud | DevSecOps Engineer**

This project demonstrates end-to-end automated infrastructure provisioning and web server deployment on AWS using native cloud automation tools.
