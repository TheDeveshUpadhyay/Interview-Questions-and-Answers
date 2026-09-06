# AWS & DevOps Engineer Interview Questions and Answers

## Overview

This document contains practical **AWS and DevOps interview questions and answers** covering real-world topics such as:

- AWS
- VPC and Networking
- EC2
- IAM and Security
- Linux
- Bash/Shell Scripting
- Python
- Terraform
- Jenkins
- CI/CD
- Amazon EKS
- Amazon S3
- AWS Secrets Manager

The answers are structured to help understand the concepts and explain them clearly during technical interviews.

---

# Q1: Are you part of requirement planning, design, deployment, or monitoring? Which one?

## Answer

I am mainly part of **deployment and monitoring activities**.

I also participate in **requirement planning discussions** and **infrastructure design** with the application and architecture teams.

My primary work includes:

- CI/CD
- AWS infrastructure
- Terraform
- Docker
- Kubernetes/EKS deployments
- Monitoring
- Troubleshooting

During requirement planning, I understand:

- Application requirements
- Infrastructure needs
- Expected traffic
- Security requirements
- Deployment strategy

In the design phase, I help decide:

- AWS services
- Kubernetes architecture
- Networking
- CI/CD flow
- Infrastructure using Terraform

My major responsibility is the **deployment phase**, where I work on CI/CD pipelines, Docker images, Kubernetes/EKS deployments, Terraform, and release activities.

After deployment, I also support **monitoring and troubleshooting** using tools such as:

- Prometheus
- Grafana
- Amazon CloudWatch

### Easy Way to Explain in an Interview

```text
Requirement
    ↓
Understand application and infrastructure needs
    ↓
Design
    ↓
Help design AWS, Kubernetes, networking and CI/CD
    ↓
Deployment
    ↓
Build pipeline → Deploy application → Manage infrastructure
    ↓
Monitoring
    ↓
Monitor application/infrastructure → Troubleshoot issues
```

---

# Q2: How are you communicating with your customers? Through private IP or public IP?

## Answer

For external customers, we normally communicate through a **public endpoint**, not directly through a private IP.

Customers access the application through a **public DNS name or public Load Balancer**.

The Load Balancer is internet-facing and receives traffic from customers.

Behind the Load Balancer, application servers or Kubernetes worker nodes usually run in **private subnets with private IP addresses**.

Therefore, customers do not directly connect to the private IP addresses.

### Simple Flow

```text
Customer
    ↓
Internet
    ↓
Public DNS
    ↓
Internet-facing ALB
    ↓
Private Subnet
    ↓
Application / EKS Pods
```

### Easy Way to Remember

```text
External Customer → Public Endpoint

Internal Communication → Private IP
```

---

# Q3: If it is a private IP, can you explain it in terms of VPCs?

## Answer

Yes. In AWS, **private IP communication happens inside a VPC**.

A VPC is a private network in AWS.

Inside a VPC, we create subnets and resources such as:

- EC2 instances
- EKS worker nodes
- Databases
- Internal Load Balancers

Resources within the same VPC can communicate using their **private IP addresses** through the VPC's internal routing.

If the customer is in another VPC or an on-premises network, private connectivity can be established using:

- VPC Peering
- Transit Gateway
- Site-to-Site VPN
- Direct Connect

We also configure **route tables and Security Groups** to allow the required traffic.

### Example

```text
VPC: 10.0.0.0/16
│
├── Public Subnet: 10.0.1.0/24
│       └── Public Load Balancer
│
└── Private Subnet: 10.0.2.0/24
        ├── Application Server: 10.0.2.10
        └── Database Server:    10.0.2.20
```

The application server can communicate with the database privately:

```text
Application Server
10.0.2.10
    ↓
VPC Internal Network
    ↓
Database Server
10.0.2.20
```

The traffic stays inside the VPC and does not need to travel through the public internet.

### If the Customer Is in Another Private Network

```text
Customer VPC
10.1.0.0/16
    ↓
VPC Peering / Transit Gateway / VPN
    ↓
Our VPC
10.0.0.0/16
```

### Easy Way to Remember

```text
Same VPC
   ↓
Private IP

Different VPC
   ↓
VPC Peering / Transit Gateway

On-Premises → AWS
   ↓
VPN / Direct Connect
```

---

# Additional Concept: What Is an Application Server and a Database Server?

## Application Server

An **Application Server** runs the actual application or backend code.

For example:

```text
Customer
   ↓
www.shop.com
   ↓
Load Balancer
   ↓
Application Server
```

The application server may run:

- Java / Spring Boot
- Python
- Node.js
- .NET

Its responsibilities may include:

- Login processing
- Order processing
- Payment logic
- Calling APIs
- Reading data from databases
- Writing data to databases

In AWS, an application server could be:

- EC2 instance
- ECS container
- EKS Pod

---

## Database Server

A **Database Server** stores the application's data.

For example:

- User information
- Password hashes
- Orders
- Product details
- Payment records
- Application data

Common databases include:

- MySQL
- PostgreSQL
- Oracle
- SQL Server
- MongoDB

In AWS, the database could be:

- Amazon RDS
- Amazon Aurora
- Database running on EC2

### Complete Request Flow

```text
Customer
   ↓
Internet
   ↓
Application Load Balancer
   ↓
Application Server
   ↓
Database Server
```

### Easy Way to Remember

```text
Application Server = Runs application/business logic

Database Server = Stores application data
```

---

# Additional Concept: What Runs in Public and Private Subnets?

A typical AWS architecture separates internet-facing resources from backend resources.

### Public Subnet

Common resources include:

- Application Load Balancer
- NAT Gateway
- Bastion Host, if required

### Private Application Subnet

Common resources include:

- EC2 application servers
- ECS Tasks
- EKS worker nodes/workloads

### Private Database Subnet

Common resources include:

- Amazon RDS
- Amazon Aurora
- Database servers

### Typical Architecture

```text
Internet
   ↓
Route 53
   ↓
Application Load Balancer
Public Subnet
   ↓
Application Server / EKS
Private Subnet
   ↓
RDS / Database
Private Subnet
```

### Important Concept

A subnet is generally considered public when its route table has a route to an **Internet Gateway**.

```text
Destination       Target
10.0.0.0/16       local
0.0.0.0/0         Internet Gateway
```

A typical private application subnet may use a NAT Gateway for outbound internet connectivity:

```text
Destination       Target
10.0.0.0/16       local
0.0.0.0/0         NAT Gateway
```

### NAT Gateway Flow

```text
EC2 in Private Subnet
        ↓
NAT Gateway
        ↓
Internet Gateway
        ↓
Internet
```

### Easy Way to Remember

```text
Internet
   ↓
Public Subnet
   ↓
ALB
   ↓
Private Application Subnet
   ↓
EC2 / ECS / EKS
   ↓
Private Database Subnet
   ↓
RDS / Aurora
```

---

# Q4: An EC2 instance is created in a private subnet. How would you connect to that EC2 instance?

## Answer

An EC2 instance in a **private subnet normally does not have a public IP**, so we cannot directly SSH to it from the internet.

One traditional method is to use a **Bastion Host / Jump Server**.

The Bastion Host is placed in a public subnet, while the target EC2 instance remains in the private subnet.

### Architecture

```text
Your Laptop
    ↓
Internet
    ↓
Bastion Host
Public Subnet
    ↓
Private IP
    ↓
EC2 Instance
Private Subnet
```

Example:

```text
Bastion Host Public IP: 13.x.x.x
Private EC2 IP:          10.0.2.10
```

Connect to the Bastion Host:

```bash
ssh -i key.pem ec2-user@13.x.x.x
```

Then connect to the private EC2 instance:

```bash
ssh ec2-user@10.0.2.10
```

AWS Systems Manager Session Manager can also be used to access EC2 instances without exposing SSH through a Bastion Host.

---

# Q5: A client wants to connect to 40 EC2 instances out of 100 EC2 instances configured in private subnets under VPN. How would you provide connectivity?

## Answer

The source document contains this interview question, but the answer section is currently empty.

To keep this README faithful to the provided interview notes, the answer should be completed separately.

---

# Q6: How would you explain the security aspects to a client who wants to migrate from on-premises to the public cloud?

## Answer

The source document contains this question, but the answer section is currently empty.

---

# Q7: A client wants to migrate from its corporate network to the public cloud. What would you suggest in terms of security?

## Answer

The source document contains this question, but the answer section is currently empty.

---

# Q8: How would you explain the different cloud security layers to a client migrating from on-premises to the cloud?

## Answer

The source document contains this question, but the answer section is currently empty.

---

# Q9: Can you create an IAM policy that identifies whether a user has logged in through a particular VPN connection and allows or denies access?

## Answer

The source document contains this question, but the answer section is currently empty.

---

# Q10: How would you create five different AWS accounts for a development team? How would you plan authentication and authorization, and what is the difference between them?

## Answer

The source document contains this question, but the answer section is currently empty.

---

# Q11: Which Linux commands would you use for the following tasks?

1. Check the current shell.
2. Check the default shell.
3. Create and edit a file.

## Answer

### 1. Check the Current Shell

```bash
echo $SHELL
```

Example output:

```text
/bin/bash
```

### 2. Check the Default Shell

The notes use:

```bash
echo $SHELL
```

Example:

```text
/bin/bash
```

### 3. Create a File

```bash
touch file.txt
```

### Edit the File

```bash
vi file.txt
```

---

# Q12: Have you done security patching in a project? If yes, how?

## Answer

The source document contains this question, but the answer section is currently empty.

---

# Q13: How can you restrict malicious IP addresses from accessing EC2 instances?

## Answer

The source document contains this question, but the answer section is currently empty.

---

# Q14: Which scripting languages do you know, and where have you used Python?

## Answer

I mainly work with **Bash/Shell scripting and Python**.

I use Bash for day-to-day Linux and CI/CD automation.

I use Python when I need more complex automation, AWS API interaction, file processing, or reusable scripts.

## Bash/Shell Scripting Use Cases

I use shell scripts for tasks such as:

- Server health checks
- Disk utilization checks
- Log cleanup
- Service restarts
- File backups
- Deployment automation
- Running Terraform commands
- Running `kubectl`
- Running AWS CLI commands

Examples:

```bash
df -h
free -m
systemctl status nginx
kubectl get pods
```

A simple automation flow can be:

```text
Jenkins
   ↓
Shell Script
   ↓
Build / Deploy / Health Check
```

## Python Use Cases

I use Python mainly for automation where shell scripting becomes difficult to maintain.

For AWS automation, Python can interact with AWS services using **boto3**.

```text
Python
   ↓
boto3
   ↓
AWS API
   ↓
EC2 / S3 / EBS / RDS
```

Python automation can be used to:

- Find stopped EC2 instances
- Create EBS snapshots
- Upload files to S3
- List AWS resources
- Check resource tags

---

# Q15: Which Python modules have you used in DevOps projects?

## Answer

Some Python modules I have used for DevOps-related automation include:

- `boto3`
- `requests`
- `os`
- `subprocess`
- `json`
- `logging`
- `datetime`
- `shutil`

## 1. boto3

Used to interact with AWS services.

Example:

```python
import boto3

ec2 = boto3.client("ec2")
```

Typical use cases:

- Start/stop EC2 instances
- Create snapshots
- Upload files to S3
- List AWS resources
- Send SNS notifications

---

## 2. requests

Used to call APIs and perform application health checks.

```python
import requests

response = requests.get("https://example.com")
print(response.status_code)
```

Typical use cases:

- API health checks
- Calling REST APIs
- Checking HTTP status codes
- Triggering external services

---

## 3. os

Used to interact with the operating system.

```python
import os

print(os.getcwd())
```

Typical use cases:

- Environment variables
- File paths
- Directories
- Operating system tasks

---

## 4. subprocess

Used when Python needs to execute Linux or DevOps commands.

```python
import subprocess

subprocess.run(["kubectl", "get", "pods"])
```

It can execute commands such as:

- `kubectl`
- `terraform`
- `aws`
- `docker`
- Linux commands

---

## 5. json

Used to read and process JSON data.

```python
import json
```

Typical use cases:

- API responses
- AWS output
- Configuration files
- Data processing

---

## 6. logging

Used to create proper automation logs.

```python
import logging

logging.info("Deployment started")
```

Common log levels include:

```text
INFO
WARNING
ERROR
DEBUG
```

---

## 7. datetime

Used for date and time operations.

```python
from datetime import datetime

print(datetime.now())
```

Typical use cases:

- Snapshot dates
- Backup timestamps
- Log timestamps
- Old file cleanup

---

## 8. shutil

Used for file and directory operations.

Typical use cases:

- Copy files
- Move files
- Delete directories
- Backup files

### Most Relevant Modules for DevOps Interviews

```text
boto3
requests
os
subprocess
json
logging
datetime
```

---

# Q16: How do you manage the Terraform state file in your environment?

## Answer

In our environment, we store Terraform state remotely in an **Amazon S3 backend** instead of keeping it locally.

We:

- Store state remotely in S3
- Enable S3 versioning
- Enable encryption
- Restrict access using IAM policies
- Use state locking
- Maintain separate state for Dev, Test, and Prod
- Never commit Terraform state files to Git

Terraform maintains a file called:

```text
terraform.tfstate
```

It records information about the infrastructure Terraform manages.

### Architecture

```text
Terraform
    ↓
S3 Bucket
    ↓
terraform.tfstate
```

Example:

```text
Bucket: company-terraform-state
Key:    prod/network/terraform.tfstate
```

### Why Use S3?

#### Centralized Storage

All engineers and CI/CD pipelines can use the same remote state.

#### Versioning

```text
terraform.tfstate
    ↓
Version 1
Version 2
Version 3
```

If state is accidentally overwritten or corrupted, an older version may potentially be restored.

#### Separate Environments

```text
Dev
 ↓
dev/terraform.tfstate

Test
 ↓
test/terraform.tfstate

Prod
 ↓
prod/terraform.tfstate
```

This helps isolate environments.

---

# Q17: What is Terraform state locking, and how can you achieve it?

## Answer

Terraform state locking ensures that **only one process can modify a particular state file at a time**.

Suppose two engineers run:

```bash
terraform apply
```

against the same environment at the same time.

Without locking, this could cause:

- Conflicting changes
- Incorrect infrastructure updates
- State corruption
- One operation interfering with another

### How State Locking Works

```text
Engineer A
    ↓
terraform apply
    ↓
State Lock Acquired 🔒
    ↓
Terraform Makes Changes
    ↓
Operation Completes
    ↓
State Lock Released 🔓
```

At the same time:

```text
Engineer B
    ↓
terraform apply
    ↓
Cannot Acquire Lock
    ↓
Wait / Operation Fails
```

## S3 Lock File

With an S3 backend, the notes use native S3 lock files:

```hcl
terraform {
  backend "s3" {
    bucket       = "company-terraform-state"
    key          = "prod/terraform.tfstate"
    region       = "ap-south-1"
    use_lockfile = true
  }
}
```

The important configuration is:

```hcl
use_lockfile = true
```

Conceptually:

```text
terraform.tfstate
terraform.tfstate.tflock
```

## Older DynamoDB-Based Setup

The notes also describe the older architecture:

```text
S3
 ↓
Stores Terraform State

DynamoDB
 ↓
State Locking
```

### Easy Way to Remember

```text
One State
   +
One Writer at a Time
   =
Safe Terraform Operations
```

---

# Q18: How do you handle manual changes made to an EC2 instance managed by Terraform?

## Answer

When someone manually changes an EC2 instance from the AWS Console while the same EC2 instance is managed by Terraform, this creates **configuration drift**.

Example Terraform configuration:

```hcl
resource "aws_instance" "app" {
  ami           = "ami-123456"
  instance_type = "t3.micro"
}
```

Terraform expects:

```text
t3.micro
```

Someone manually changes it to:

```text
t3.large
```

Now:

```text
Terraform Code = t3.micro
Actual AWS EC2 = t3.large
```

This difference is called **configuration drift**.

## Identify the Drift

Run:

```bash
terraform plan
```

Terraform compares the configuration with the actual infrastructure.

Conceptually:

```text
Terraform Code
      ↓
    Compare
      ↑
Actual AWS Infrastructure
      ↓
terraform plan
```

Terraform may show:

```text
t3.large → t3.micro
```

This indicates that the actual infrastructure differs from the Terraform configuration.

---

## What If Someone Created a New EC2 Instance Manually?

If an EC2 instance already exists in AWS but Terraform did not create it, you can bring it under Terraform management using:

```bash
terraform import
```

Example:

```bash
terraform import aws_instance.app i-0123456789
```

### Flow

```text
Existing EC2 in AWS
        ↓
terraform import
        ↓
Terraform State
        ↓
Terraform Knows About EC2
```

`terraform import` does **not create a new EC2 instance**.

It associates an existing AWS resource with a Terraform resource in state.

After importing, run:

```bash
terraform plan
```

Review any differences carefully.

### Easy Way to Remember

```text
terraform apply
    =
Create/change infrastructure using Terraform

terraform import
    =
Bring existing infrastructure under Terraform management
```

---

# Q19: Why do we need Terraform modules?

## Answer

A Terraform module is used to **reuse infrastructure code** instead of writing the same Terraform resources repeatedly.

Think of a module as a **reusable infrastructure template**.

Terraform modules help with:

- Code reuse
- Reduced duplication
- Standardization
- Maintainability
- Cleaner project organization

### Example

Without modules:

```text
Dev  → EC2 code

Test → Same EC2 code

Prod → Same EC2 code
```

With a module:

```text
        Reusable EC2 Module
               ↓
        ┌──────┼──────┐
        ↓      ↓      ↓
       Dev    Test   Prod
```

We write the infrastructure logic once and reuse it with different input variables.

### Easy Way to Remember

```text
Reuse
 ↓
Less Duplication

Standardization
 ↓
Same Architecture

Maintenance
 ↓
Change Code in One Place
```

---

# Q20: How are you deploying changes through Jenkins?

## Answer

In Jenkins, we deploy changes through a **CI/CD pipeline defined in a Jenkinsfile**.

### CI/CD Flow

```text
Developer Changes Code
        ↓
Pushes Code to GitHub
        ↓
GitHub Webhook
        ↓
Jenkins Pipeline
        ↓
Checkout Code
        ↓
Build
        ↓
Test
        ↓
Build Docker Image
        ↓
Push Image to Amazon ECR
        ↓
Deploy to Amazon EKS
        ↓
Verify Rollout
```

The process is:

1. Developer pushes code to GitHub.
2. GitHub webhook triggers Jenkins.
3. Jenkins checks out the latest code.
4. Jenkins builds the application.
5. Jenkins runs tests.
6. Jenkins creates a Docker image.
7. Jenkins pushes the image to Amazon ECR.
8. Jenkins deploys the new image to EKS using `kubectl` or Helm.
9. Kubernetes performs the rollout.
10. We verify the deployment and application health.

If deployment fails, we can roll back to the previous stable version.

---

# Q21: Do you use Terraform, scripting, or CLI commands to deploy through Jenkins?

## Answer

We use different tools for different stages.

### Terraform

Used for **infrastructure provisioning**.

### CLI Commands

Tools such as:

- `kubectl`
- Helm
- AWS CLI

are used for application deployment and infrastructure operations.

### Shell Scripts

Shell scripts can combine multiple commands and automation steps.

### Jenkins

Jenkins orchestrates the complete CI/CD workflow.

### Example Flow

```text
Developer Pushes Code
        ↓
Jenkins Pipeline
        ↓
Build
        ↓
Test
        ↓
Docker Image Build
        ↓
Push Image to ECR
        ↓
Deploy to EKS using kubectl/Helm
```

### Easy Way to Remember

```text
Terraform
    =
Infrastructure Provisioning

CLI
    =
Execute Deployment Commands

Shell Script
    =
Combine Multiple Commands

Jenkins
    =
Orchestrates Everything
```

---

# Q22: How is GitHub connected to Jenkins? Is it pull-based or push-based?

## Answer

Usually, **GitHub-to-Jenkins triggering is push-based using a webhook, but Jenkins pulls the source code from GitHub**.

Both concepts are involved.

## Push-Based Trigger

When a developer pushes code:

```text
Developer
   ↓
git push
   ↓
GitHub
   ↓
Webhook
   ↓
Jenkins
   ↓
Pipeline Starts
```

GitHub notifies Jenkins that new code has been pushed.

This is **push-based triggering**.

## Jenkins Pulls the Source Code

After receiving the webhook, Jenkins retrieves the source code using operations such as:

```bash
git clone
```

or:

```bash
git checkout
```

### Complete Flow

```text
Developer
   ↓
Push Code
   ↓
GitHub
   ↓
Webhook Notification
   ↓
Jenkins
   ↓
Pull Source Code
   ↓
Build
   ↓
Test
   ↓
Deploy
```

## Webhook vs Poll SCM

| Feature | Webhook | Poll SCM |
|---|---|---|
| Trigger | Push-based | Pull-based checking |
| Action | GitHub notifies Jenkins | Jenkins checks GitHub |
| Timing | Near real-time | Runs on schedule |
| Efficiency | More efficient | More unnecessary checks |
| Usage | Commonly preferred | Useful when webhook is unavailable |

### Easy Way to Remember

```text
Webhook

GitHub → Jenkins
= Push-based trigger

Poll SCM

Jenkins → GitHub
= Pull-based checking

After Trigger

Jenkins → GitHub
= Pull source code
```

---

# Q23: Where do you store project-related secrets and tokens in cloud environments?

## Answer

Project-related secrets and tokens should **not be stored directly in source code or Git repositories**.

Secure secret-management services can include:

- AWS Secrets Manager
- AWS Systems Manager Parameter Store

For CI/CD tools, use their secure credential stores, such as:

- Jenkins Credentials
- GitHub Actions Secrets

### Simple Flow

```text
Application / Pipeline
        ↓
Secret Management Service
        ↓
Required Secret
```

---

# Q24: Where would you store application-level secrets if the application is running on EC2?

## Answer

For an application running on EC2, I would normally use **AWS Secrets Manager**.

Secrets should not be hardcoded inside application code.

Examples of application secrets include:

- Database username/password
- API keys
- Access tokens
- Third-party credentials
- Private keys
- Application credentials

Instead of storing something like:

```text
DB_PASSWORD=MyPassword123
```

inside the application, store it securely in AWS Secrets Manager.

### Architecture

[O```text
Application
    ↓
EC2 Instance
    ↓
IAM Role
    ↓
AWS Secrets Manager
    ↓
Database Credentials
```

The EC2 application requests the secret when required.

## Why Is an IAM Role Required?

The EC2 instance needs permission to read the secret.

Example:

```text
EC2 Instance
    ↓
IAM Role
    ↓
secretsmanager:GetSecretValue
    ↓
AWS Secrets Manager
```

The IAM role should only allow access to the required secret.

For example:

```text
Application-EC2-Role
        ↓
Can Read
        ↓
prod/database/password
```

It should not automatically have permission to read every secret in the AWS account.

This follows the **principle of least privilege**.

---

# Q25: What security features of Amazon S3 can be applied to an application?

## Answer

For an application using Amazon S3, security can be applied mainly at the:

- Access level
- Network level
- Encryption level
- Auditing level

The provided notes explain the following controls in detail.

## 1. S3 Block Public Access

For application data, normally enable:

**S3 Block Public Access**

This helps prevent the bucket or objects from accidentally becoming publicly accessible.

```text
Internet
   ❌
S3 Bucket
```

Unless files genuinely need to be public, keep the bucket private.

---

## 2. IAM Roles and Least Privilege

The application should not automatically receive full S3 access.

For example, if it only needs to upload and read objects:

```text
s3:GetObject
s3:PutObject
```

Avoid granting:

```text
s3:*
```

unless it is genuinely required.

### Architecture

```text
EC2 / EKS / Lambda
        ↓
IAM Role
        ↓
Required S3 Permissions Only
        ↓
Amazon S3
```

---

## 3. S3 Versioning

Versioning helps protect data against accidental overwrite or deletion.

```text
report.txt
    ↓
Version 1
Version 2
Version 3
```

If an object is overwritten or deleted, an older version may potentially be restored.

Versioning is mainly a **data protection and recovery feature**, rather than an access-control feature.

---

## 4. S3 VPC Endpoint

If the application runs inside a VPC, an S3 VPC Endpoint can be used.

```text
Application
Private Subnet
      ↓
S3 VPC Endpoint
      ↓
Amazon S3
```

This allows the application to access S3 without requiring that traffic to travel through a NAT Gateway or the public internet.

### Easy Way to Remember

```text
Public Access
     ↓
Block It

Permissions
     ↓
IAM + Bucket Policy

Network
     ↓
VPC Endpoint

Recovery
     ↓
Versioning
```

For an application running on EC2 or EKS, use an **IAM role instead of storing AWS access keys in application code**.

Grant only the S3 permissions the application actually requires.

---

# Quick Interview Revision

| Topic | Key Point |
|---|---|
| Customer Access | Public endpoint / Load Balancer |
| Internal Communication | Private IP |
| VPC | Private AWS network |
| Private EC2 Access | Bastion Host / Session Manager |
| Linux | `echo $SHELL`, `touch`, `vi` |
| Python AWS Automation | `boto3` |
| Terraform State | Remote S3 backend |
| Terraform Locking | Prevent concurrent state modification |
| Configuration Drift | Detect using `terraform plan` |
| Terraform Import | Bring existing resources under Terraform management |
| Terraform Modules | Reusable infrastructure code |
| Jenkins | CI/CD orchestration |
| GitHub → Jenkins | Webhook is push-based |
| Jenkins → GitHub | Jenkins pulls source code |
| Application Secrets | AWS Secrets Manager |
| S3 Access | IAM + least privilege |
| S3 Private Connectivity | VPC Endpoint |
| S3 Recovery | Versioning |

---

# Key Takeaways

- Understand the **concept**, not only the command.
- Explain answers using a simple **real-world architecture or flow**.
- Follow the **principle of least privilege** for AWS access.
- Keep application servers and databases protected in **private subnets** where appropriate.
- Use **Terraform remote state and locking** for team environments.
- Avoid manual infrastructure changes that create **configuration drift**.
- Use **CI/CD pipelines** to automate build, test, and deployment.
- Never hardcode **passwords, tokens, API keys, or AWS credentials** in source code.

---

## Interview Preparation Tip

For scenario-based questions, structure your answer as:

```text
Understand the requirement/problem
        ↓
Check the relevant service/component
        ↓
Identify the root cause or security requirement
        ↓
Apply the appropriate solution
        ↓
Validate
```

---

## Topics Covered

`AWS` `DevOps` `VPC` `EC2` `IAM` `Linux` `Python` `Terraform` `Jenkins` `CI/CD` `Docker` `EKS` `S3` `Secrets Manager`

---

> **Note:** Questions Q5, Q6, Q7, Q8, Q9, Q10, Q12, and Q13 have questions but no answers in the provided source notes. They have intentionally been left as pending rather than adding answers that were not present in the source material.
