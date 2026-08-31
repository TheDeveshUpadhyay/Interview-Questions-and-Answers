# Infosys AWS Engineer – Interview Experience

## Interview Overview

| Details                | Information                                                                |
| ---------------------- | -------------------------------------------------------------------------- |
| **Company**            | Infosys                                                                    |
| **Role**               | AWS Engineer                                                               |
| **Interview Duration** | 38 Minutes                                                                 |
| **Topics Covered**     | AWS, Kubernetes, Terraform, Networking, Infrastructure, Project Experience |

This document contains my **Infosys AWS Engineer interview experience** and the questions discussed during the interview.

The interview focused on both **technical concepts and real-world project experience**, particularly around:

* AWS
* Kubernetes
* Amazon EKS
* AWS Networking
* Kubernetes Upgrades
* Kubernetes Autoscaling
* Terraform
* Terraform State Management
* Infrastructure Troubleshooting
* Project Experience

---

# Interview Questions

## 1. Introduce Yourself

The interviewer started with the standard question:

> **Tell me about yourself.**

### What the interviewer expects

The introduction should be short, structured, and relevant to the AWS Engineer position.

A good introduction should cover:

* Total IT experience
* AWS/Cloud experience
* DevOps experience
* Key technical skills
* Current or recent project
* Major responsibilities
* Relevant certifications

### Recommended Structure

```text
Introduction
     ↓
Total Experience
     ↓
AWS / DevOps Experience
     ↓
Key Technologies
     ↓
Current Project
     ↓
Major Responsibilities
     ↓
Certifications
```

### Important

Do not spend too much time discussing personal information.

Focus on your **professional experience, technical skills, and project responsibilities** relevant to the position.

---

# 2. What Projects Have You Worked On?

The interviewer asked about previous projects.

### What to Explain

For each major project, be prepared to explain:

* Project objective
* Business requirement
* Application architecture
* Infrastructure architecture
* Your role
* AWS services used
* DevOps tools used
* CI/CD implementation
* Infrastructure automation
* Kubernetes implementation
* Monitoring
* Security
* Troubleshooting
* Major challenges

### Example Project Flow

```text
Business Requirement
        ↓
Application Architecture
        ↓
AWS Infrastructure
        ↓
CI/CD Pipeline
        ↓
Build & Test
        ↓
Docker Image
        ↓
Container Registry
        ↓
Kubernetes / EKS
        ↓
Application Deployment
        ↓
Monitoring
        ↓
Troubleshooting
```

### Important

Do not simply say:

> I worked on AWS and Kubernetes.

Be prepared to explain:

* What you implemented
* Why you implemented it
* How you implemented it
* What problems you faced
* How you solved those problems

---

# 3. What AWS Services Have You Worked With?

The interviewer may expect you to explain the AWS services you have actually used.

## Common AWS Services

| AWS Service      | Typical Usage                  |
| ---------------- | ------------------------------ |
| **EC2**          | Compute                        |
| **VPC**          | Network infrastructure         |
| **IAM**          | Identity and access management |
| **S3**           | Object storage                 |
| **EBS**          | Block storage                  |
| **RDS**          | Managed databases              |
| **ELB**          | Load balancing                 |
| **Auto Scaling** | Automatic capacity management  |
| **Route 53**     | DNS management                 |
| **CloudWatch**   | Monitoring and logging         |
| **EKS**          | Managed Kubernetes             |
| **SNS**          | Notifications                  |

### Interview Tip

Do not just memorize a list of AWS services.

If you mention a service, expect follow-up questions such as:

* Why did you use it?
* How did you configure it?
* What problem did it solve?
* What alternatives were available?
* What challenges did you face?
* How did you troubleshoot it?

The interviewer is generally more interested in **hands-on experience** than memorized definitions.

---

# 4. Describe the Recent Project/Work You Were Involved In

The interviewer asked about the most recent project.

A good answer should explain the project from both the **business and technical perspective**.

## Project Overview

Explain:

* What the application does
* Who uses the application
* Application architecture
* Infrastructure architecture
* Deployment architecture

## Your Responsibilities

Depending on your actual experience, responsibilities may include:

* AWS infrastructure management
* Kubernetes administration
* EKS cluster management
* CI/CD pipeline management
* Terraform automation
* Docker image management
* Application deployment
* Monitoring
* Logging
* Troubleshooting
* Security configuration
* Incident resolution

### Example CI/CD Flow

```text
Developer
    ↓
Git Repository
    ↓
CI/CD Pipeline
    ↓
Build
    ↓
Test
    ↓
Code Quality Analysis
    ↓
Docker Build
    ↓
Container Registry
    ↓
Kubernetes / EKS
    ↓
Application Deployment
    ↓
Monitoring
```

---

# 5. What Challenges Did You Encounter in Your Recent Project, and How Did You Resolve Them?

This is an important **scenario-based interview question**.

Avoid answering:

> I didn't face any major challenges.

Production environments always have challenges.

The interviewer wants to understand your **problem-solving and troubleshooting approach**.

## Recommended Approach

```text
Problem
   ↓
Investigation
   ↓
Root Cause
   ↓
Solution
   ↓
Validation
   ↓
Prevention
```

### Example

Suppose an application deployment is failing.

A structured troubleshooting approach could be:

1. Check the Kubernetes Pod status.
2. Check Pod events.
3. Review container logs.
4. Check application configuration.
5. Check networking and dependencies.
6. Identify the root cause.
7. Correct the configuration.
8. Redeploy the application.
9. Verify application health.
10. Add preventive monitoring or validation.

### Key Point

Do not only explain:

> What was the solution?

Explain:

> **How did you identify the root cause?**

That demonstrates real troubleshooting experience.

---

# Kubernetes Interview Questions

# 6. What Challenges Do You Typically Encounter During a Kubernetes Upgrade?

Kubernetes upgrades can affect multiple components of the cluster.

## Common Challenges

* Kubernetes API deprecations
* Deprecated API versions
* Control plane compatibility
* Worker node compatibility
* CNI compatibility
* CSI driver compatibility
* CoreDNS compatibility
* kube-proxy compatibility
* Ingress Controller compatibility
* Helm chart compatibility
* Custom Resource Definition (CRD) compatibility
* Application compatibility
* PodDisruptionBudget behavior
* Workload availability
* Monitoring compatibility

## Kubernetes Upgrade Approach

A safer upgrade process can look like:

```text
Check Current Version
        ↓
Review Release Notes
        ↓
Check Deprecated APIs
        ↓
Check Application Compatibility
        ↓
Check Add-ons
        ↓
Backup / Recovery Plan
        ↓
Upgrade
        ↓
Validate Cluster
        ↓
Validate Applications
        ↓
Monitor
```

### Important

A Kubernetes upgrade should not be treated as:

```text
Upgrade Version
      ↓
Done
```

A production upgrade requires:

* Planning
* Compatibility checks
* Backup/recovery planning
* Controlled execution
* Validation
* Monitoring

---

# 7. What Checks Do You Perform After a Kubernetes Upgrade?

After upgrading Kubernetes, verify both the **cluster components and application workloads**.

## Check Nodes

```bash
kubectl get nodes
```

Verify that the expected nodes are:

```text
Ready
```

## Check All Pods

```bash
kubectl get pods -A
```

Look for problematic states such as:

* `CrashLoopBackOff`
* `ImagePullBackOff`
* `Pending`
* `Error`
* `ContainerCreating`
* `Terminating`

## Check Kubernetes System Components

```bash
kubectl get pods -n kube-system
```

Check components such as:

* CoreDNS
* kube-proxy
* CNI
* CSI drivers
* Other cluster add-ons

## Check Cluster Information

```bash
kubectl cluster-info
```

## Check Events

```bash
kubectl get events -A
```

## Check Services

```bash
kubectl get svc -A
```

## Check Ingress

```bash
kubectl get ingress -A
```

## Check Storage

```bash
kubectl get pv
kubectl get pvc -A
```

## Application Validation

Verify:

* Application Pods
* Services
* Ingress
* DNS
* Networking
* Persistent Volumes
* Readiness probes
* Liveness probes
* Application endpoints
* Logs
* Monitoring
* Error rates

---

# 8. What Was the Kubernetes Version Before the Upgrade, and Which Version Did You Upgrade To?

This is an **experience-based question**.

The interviewer wants to determine whether you have actually worked on Kubernetes upgrades.

Be prepared to explain:

```text
Previous Kubernetes Version
          ↓
Target Kubernetes Version
          ↓
Reason for Upgrade
          ↓
Pre-Upgrade Checks
          ↓
Upgrade Process
          ↓
Challenges Encountered
          ↓
Post-Upgrade Validation
          ↓
Final Result
```

## Example Answer Structure

> The cluster was running Kubernetes version X, and we upgraded it to version Y because of support lifecycle, security updates, feature requirements, or compatibility requirements. Before the upgrade, we reviewed deprecated APIs and checked the compatibility of add-ons and workloads. After the upgrade, we validated nodes, Pods, networking, DNS, storage, and application health.

### Important

Do not invent Kubernetes versions.

If you have not personally performed an upgrade, explain your actual involvement honestly.

---

# 9. What Checks Do You Perform After the Upgrade to Ensure Everything Is Working Correctly?

Post-upgrade validation should cover both **infrastructure and application workloads**.

## 1. Validate Nodes

```bash
kubectl get nodes
```

Check that all expected nodes are `Ready`.

## 2. Validate Pods

```bash
kubectl get pods -A
```

Look for failed or unhealthy workloads.

## 3. Validate System Components

```bash
kubectl get pods -n kube-system
```

Check:

* CoreDNS
* CNI
* kube-proxy
* CSI components
* Other cluster add-ons

## 4. Validate Services

```bash
kubectl get svc -A
```

## 5. Validate Ingress

```bash
kubectl get ingress -A
```

## 6. Validate Persistent Storage

```bash
kubectl get pv
kubectl get pvc -A
```

## 7. Validate DNS

Test Kubernetes service discovery from inside the cluster.

Example:

```bash
nslookup backend-service
```

## 8. Validate Application Health

Check:

* Application endpoints
* Readiness probes
* Liveness probes
* Application logs
* Error rates
* Response times

## 9. Validate Monitoring

Check:

* Metrics
* Dashboards
* Alerts
* Application logs
* Infrastructure monitoring

### Goal

The objective is to verify:

```text
Kubernetes Infrastructure
          +
Application Workloads
          =
Healthy Environment
```

---

# 10. What Is the Difference Between Managed and Self-Managed Nodes?

This is a common AWS EKS interview question.

## Managed Nodes

With Amazon EKS Managed Node Groups, AWS manages significant parts of the node lifecycle.

AWS provides support for areas such as:

* Node provisioning
* Node replacement
* Integration with EKS
* Node lifecycle management
* AMI management options
* Scaling workflows

The customer still controls important configuration such as:

* Instance types
* Scaling configuration
* Labels
* Taints
* Networking
* Workload placement
* Node group configuration

## Self-Managed Nodes

With self-managed nodes, the customer has more responsibility for the EC2 worker nodes.

Responsibilities can include:

* EC2 instance management
* AMI management
* Node bootstrapping
* Patching
* Scaling
* Node replacement
* Node upgrades
* Lifecycle management
* Troubleshooting

## Comparison

| Area                     | Managed Nodes            | Self-Managed Nodes        |
| ------------------------ | ------------------------ | ------------------------- |
| **Node lifecycle**       | More AWS-managed         | Customer-managed          |
| **Maintenance**          | Lower operational effort | Higher operational effort |
| **Control**              | Less customization       | More control              |
| **Upgrades**             | Easier operationally     | More responsibility       |
| **Patching**             | Simplified               | Customer responsibility   |
| **Operational overhead** | Lower                    | Higher                    |
| **Customization**        | More limited             | Greater flexibility       |

### Simple Explanation

```text
Managed Node Group
        ↓
AWS manages more of the node lifecycle
        ↓
Lower operational effort


Self-Managed Node
        ↓
Customer manages more of the node lifecycle
        ↓
Greater control + greater responsibility
```

---

# AWS Networking Interview Questions

# 11. What Is the CIDR Range of Your Subnet?

CIDR stands for:

> **Classless Inter-Domain Routing**

A subnet CIDR defines the range of IP addresses available within the subnet.

## Example

```text
10.0.1.0/24
```

A `/24` IPv4 network contains:

```text
256 total IP addresses
```

However, AWS reserves some IP addresses in each subnet, so the number of usable addresses is lower than the total.

## Example VPC Structure

A VPC might have:

```text
VPC
10.0.0.0/16
```

And subnets such as:

```text
Private Subnet 1
10.0.1.0/24
```

```text
Private Subnet 2
10.0.2.0/24
```

```text
Public Subnet 1
10.0.3.0/24
```

## Interview Follow-Up Questions

The interviewer may ask:

* What is a VPC CIDR?
* What is a subnet CIDR?
* How do you calculate IP addresses?
* What is a public subnet?
* What is a private subnet?
* What is a route table?
* What is an Internet Gateway?
* What is a NAT Gateway?
* How does traffic flow from a private subnet to the internet?

---

# 12. How Many Route Tables Can a Subnet Be Associated With?

A subnet can be associated with **only one route table at a time**.

However:

> **One route table can be associated with multiple subnets.**

## Example

```text
             Route Table
                  |
          ┌───────┴───────┐
          ↓               ↓
       Subnet A         Subnet B
```

Both Subnet A and Subnet B can use the same route table.

## Main Route Table

If a subnet does not have an explicit route table association, it uses the VPC's **main route table**.

### Key Point

```text
One Subnet
    ↓
One Route Table Association
```

But:

```text
One Route Table
    ↓
Multiple Subnets
```

---

# 13. If You Need to Make Changes to a Route Table, Would You Modify the Existing One or Create a New One? Why?

There is no universal answer.

The decision depends on the architecture and the impact of the change.

Consider:

* How many subnets use the route table?
* Is the route table shared?
* Should the change apply to all associated subnets?
* Is the change production-critical?
* Does the change introduce security risks?
* Does only one subnet require different routing?
* What is the blast radius?

## Modify the Existing Route Table

Modify the existing route table when:

* The change should apply to all associated subnets.
* The existing architecture already supports the required routing.
* The change has been reviewed.
* The impact is understood.

## Create a New Route Table

Create a new route table when:

* Only one or a subset of subnets needs different routing.
* Existing subnets should not be affected.
* Isolation is required.
* The existing route table is shared by unrelated workloads.

## Example

Current architecture:

```text
Existing Route Table
        |
   ┌────┼────┐
   ↓    ↓    ↓
Subnet A  Subnet B  Subnet C
```

If only Subnet C requires different routing:

```text
Existing Route Table
        |
   ┌────┴────┐
   ↓         ↓
Subnet A   Subnet B


New Route Table
        |
        ↓
     Subnet C
```

### Key Principle

> **Do not modify a shared production route table blindly.**

A route-table change can affect multiple subnets and multiple workloads.

---

# 14. What Would You Do If the Existing Route Table Does Not Allow the Required Modification?

First, identify **why the required routing change cannot be implemented**.

## Investigation Steps

1. Review the existing route table.
2. Check existing routes.
3. Check route targets.
4. Check subnet associations.
5. Check whether the route table is the main route table.
6. Review the VPC architecture.
7. Check security requirements.
8. Understand the impact on other subnets.

If the required routing behavior is different from the existing design, consider creating a separate route table.

## Possible Approach

```text
Understand Requirement
        ↓
Review Existing Route Table
        ↓
Check Associated Subnets
        ↓
Assess Impact
        ↓
Create New Route Table if Required
        ↓
Add Required Routes
        ↓
Associate Required Subnet
        ↓
Test Connectivity
        ↓
Monitor
```

### Important

Do not make a route-table change simply because it works technically.

First understand:

> **What other workloads could be affected?**

The objective is to minimize the **blast radius** of infrastructure changes.

---

# Kubernetes Cluster Management

# 15. Have You Ever Created a Kubernetes Cluster? What Steps Would You Consider When Creating One?

When creating a Kubernetes cluster, consider the infrastructure, networking, security, compute, scaling, and observability requirements.

## 1. Kubernetes Version

Choose a supported Kubernetes version.

Consider:

* Application compatibility
* Add-on compatibility
* Support lifecycle
* Upgrade strategy

## 2. Networking

Plan:

* VPC
* Subnets
* Availability Zones
* CIDR ranges
* Kubernetes networking
* CNI
* Security Groups

## 3. Control Plane

For Amazon EKS, AWS manages the Kubernetes control plane.

Consider:

* Control plane configuration
* API endpoint access
* Logging
* Security

## 4. Worker Nodes

Choose the appropriate compute model:

* EKS Managed Node Groups
* Self-managed nodes
* AWS Fargate where appropriate

Consider:

* Instance types
* Capacity
* Scaling
* Workload requirements
* Availability Zones

## 5. IAM

Configure:

* Cluster IAM roles
* Node IAM roles
* Pod-level permissions where required
* Least-privilege access

## 6. Add-ons

Consider:

* VPC CNI
* CoreDNS
* kube-proxy
* EBS CSI Driver
* Ingress Controller
* Monitoring tools

## 7. Security

Plan:

* Security Groups
* Network Policies
* IAM
* Secrets
* Encryption
* Least privilege
* API endpoint access

## 8. Scaling

Consider:

* Horizontal Pod Autoscaler
* Node Autoscaling
* Cluster Autoscaler
* Karpenter
* Resource Requests and Limits

## 9. Observability

Implement:

* Metrics
* Logs
* Alerts
* Dashboards
* Application monitoring

## 10. Application Deployment

Applications can be deployed using:

* Kubernetes manifests
* Helm
* GitOps tools
* CI/CD pipelines

## Overall Architecture

```text
AWS VPC
   |
   ├── Availability Zone 1
   │       └── Kubernetes Nodes
   |
   ├── Availability Zone 2
   │       └── Kubernetes Nodes
   |
   └── Availability Zone 3
           └── Kubernetes Nodes

                ↓

          EKS Control Plane

                ↓

          Applications / Pods

                ↓

        Load Balancer / Ingress

                ↓

             Users
```

---

# 16. How Would You Configure Autoscaling Policies for a Kubernetes Cluster?

Kubernetes autoscaling can happen at different levels.

## Horizontal Pod Autoscaler (HPA)

HPA automatically increases or decreases the number of Pod replicas based on metrics such as CPU or memory utilization.

### Example Flow

```text
Application Traffic Increases
          ↓
Resource Utilization Increases
          ↓
HPA Detects Higher Utilization
          ↓
More Pod Replicas
          ↓
Application Handles More Load
```

## Example HPA Configuration

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler

metadata:
  name: app-hpa

spec:
  minReplicas: 2
  maxReplicas: 10

  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: app-deployment
```

## Node Autoscaling

Sometimes Pods cannot be scheduled because there is not enough node capacity.

In that situation, node-level autoscaling can add capacity.

Common approaches include:

* Cluster Autoscaler
* Karpenter

### Complete Scaling Flow

```text
Traffic Increases
       ↓
HPA
       ↓
More Pods
       ↓
Insufficient Node Capacity
       ↓
Node Autoscaler
       ↓
More Nodes
       ↓
Pods Get Scheduled
```

### Key Point

Pod autoscaling and node autoscaling solve different problems:

```text
HPA
 ↓
Scales Pods


Node Autoscaler
 ↓
Scales Compute Capacity
```

---

# 17. What Are the Different Ways You Can Create a Kubernetes Cluster?

There are multiple ways to create a Kubernetes cluster.

## Amazon EKS

An EKS cluster can be created using:

* AWS Management Console
* AWS CLI
* `eksctl`
* Terraform
* CloudFormation

## Using eksctl

Example:

```bash
eksctl create cluster
```

`eksctl` is a command-line utility designed to simplify the creation and management of Amazon EKS clusters.

## Using Terraform

Terraform can be used to define infrastructure as code.

Terraform can manage:

* VPC
* Subnets
* EKS Cluster
* Node Groups
* IAM
* Security Groups
* Add-ons
* Networking

### Example Architecture

```text
Terraform
    ↓
VPC
    ↓
Subnets
    ↓
EKS Cluster
    ↓
Node Groups
    ↓
Kubernetes Workloads
```

## Using kubeadm

Kubernetes can also be installed using `kubeadm`.

This approach provides more control but also requires significantly more operational responsibility.

## Other Managed Kubernetes Services

Other cloud providers offer managed Kubernetes services.

Examples include:

* Amazon EKS
* Google Kubernetes Engine (GKE)
* Azure Kubernetes Service (AKS)

### Key Point

The right approach depends on:

* Environment
* Automation requirements
* Cloud provider
* Team expertise
* Infrastructure-as-Code strategy
* Operational requirements

---

# 18. How Many Kubernetes Clusters Are You Currently Managing?

This is primarily an **experience-based question**.

The interviewer wants to understand:

* Your operational experience
* Environment scale
* Production exposure
* Cluster management responsibilities

Do not answer with only a number.

Explain the environment.

## Example Structure

```text
Development
     ↓
Testing
     ↓
Staging
     ↓
Production
```

Be prepared to discuss:

* Number of clusters
* Kubernetes versions
* Number of nodes
* Production vs non-production
* Workloads
* Cluster upgrades
* Monitoring
* Security
* Incident management
* Scaling
* Troubleshooting

### Important

If you mention multiple clusters, expect follow-up questions such as:

> How are the clusters different?

> How do you manage their configurations?

> How do you perform upgrades?

> How do you monitor them?

> How do you manage access?

---

# Terraform Interview Questions

# 19. How Do You Handle Conflicts When Multiple People Are Trying to Modify Infrastructure Using Terraform?

Terraform uses a **state file** to track the infrastructure it manages.

If multiple engineers run Terraform against the same infrastructure without proper controls, they can create:

* State conflicts
* Race conditions
* Unexpected infrastructure changes
* State corruption risks
* Configuration drift

## Remote State

A common AWS approach is storing Terraform state remotely.

For example:

```text
Terraform
    ↓
Remote Backend
    ↓
Amazon S3
```

## State Locking

State locking helps prevent multiple Terraform operations from modifying the same state simultaneously.

The exact locking mechanism depends on the Terraform version and backend configuration being used.

## Recommended Practices

### 1. Use Remote State

Do not keep production Terraform state only on an engineer's local machine.

### 2. Use State Locking

Use a supported state-locking mechanism to prevent concurrent modifications.

### 3. Use Version Control

Store Terraform configuration in Git.

```text
Terraform Code
      ↓
Git Repository
      ↓
Pull Request
      ↓
Review
      ↓
Terraform Plan
      ↓
Approval
      ↓
Terraform Apply
```

### 4. Review Terraform Plan

Before applying infrastructure changes:

```bash
terraform plan
```

Review the proposed changes.

### 5. Control Production Access

Not every engineer should have permission to execute:

```bash
terraform apply
```

against production.

### 6. Use CI/CD

Terraform changes can be executed through a controlled CI/CD process.

## Example Workflow

```text
Developer
    ↓
Terraform Code
    ↓
Git Pull Request
    ↓
Code Review
    ↓
Terraform Plan
    ↓
Approval
    ↓
Terraform Apply
    ↓
Remote State
```

### Key Principle

> **Infrastructure changes should be controlled, reviewed, synchronized, and auditable.**

---

# 20. How Do You Secure a Terraform State File?

Terraform state can contain sensitive information depending on the infrastructure being managed.

Therefore, the state file must be protected carefully.

## Store State Remotely

For AWS environments, a common approach is storing Terraform state in an Amazon S3 bucket.

```text
Terraform
     ↓
S3 Remote State
     ↓
Encryption
     ↓
Restricted IAM Access
```

## Security Measures

### 1. Restrict IAM Access

Only authorized users and automation should access the Terraform state.

Follow:

> **Principle of Least Privilege**

### 2. Enable Encryption

Enable encryption for the S3 bucket containing Terraform state.

### 3. Enable Versioning

S3 versioning can help recover previous versions of the state.

### 4. Block Public Access

The Terraform state bucket must not be publicly accessible.

### 5. Monitor Access

Use appropriate AWS monitoring and auditing mechanisms to track access to the state bucket.

### 6. Avoid Committing State to Git

Do not commit Terraform state files into a Git repository.

Add state files to `.gitignore` where appropriate.

Example:

```gitignore
*.tfstate
*.tfstate.*
.terraform/
```

### 7. Protect Sensitive Outputs

Be careful with Terraform outputs and logs because sensitive values can potentially be exposed if handled incorrectly.

## Recommended Architecture

```text
                 Terraform
                     |
                     ↓
             Remote State Backend
                     |
                     ↓
                Amazon S3
                     |
          ┌──────────┼──────────┐
          ↓          ↓          ↓
     Encryption   Versioning   IAM
                                |
                                ↓
                         Least Privilege
```

---

# Complete Interview Question List

For quick revision, here are all 20 questions covered during the interview.

## Project & Experience

1. Introduce yourself.
2. What projects have you worked on?
3. What AWS services have you worked with?
4. Describe the recent project/work you were involved in.
5. What challenges did you encounter in your recent project, and how did you resolve them?

## Kubernetes

6. What challenges do you typically encounter during a Kubernetes upgrade?
7. What checks do you perform after a Kubernetes upgrade?
8. What was the Kubernetes version before the upgrade, and which version did you upgrade to?
9. What checks do you perform after the upgrade to ensure everything is working correctly?
10. What is the difference between managed and self-managed nodes?
11. Have you ever created a Kubernetes cluster? What steps would you consider when creating one?
12. How would you configure autoscaling policies for a Kubernetes cluster?
13. What are the different ways to create a Kubernetes cluster?
14. How many Kubernetes clusters are you currently managing?

## AWS Networking

11. What is the CIDR range of your subnet?
12. How many route tables can a subnet be associated with?
13. If you need to make changes to a route table, would you modify the existing one or create a new one? Why?
14. What would you do if the existing route table does not allow the required modification?

## Terraform

19. How do you handle conflicts when multiple people are trying to modify infrastructure using Terraform?
20. How do you secure a Terraform state file?

---

# Key Interview Takeaways

This interview covered four major areas:

```text
AWS
 │
 ├── VPC
 ├── Subnets
 ├── CIDR
 ├── Route Tables
 └── Infrastructure

Kubernetes
 │
 ├── Cluster Creation
 ├── Cluster Upgrades
 ├── Nodes
 ├── Autoscaling
 ├── Validation
 └── Cluster Management

Terraform
 │
 ├── State Management
 ├── Remote State
 ├── State Locking
 ├── Collaboration
 └── State Security

Project Experience
 │
 ├── Architecture
 ├── Responsibilities
 ├── Challenges
 ├── Troubleshooting
 └── Production Experience
```

---

# Important Preparation Areas

If you are preparing for an **AWS Engineer, Cloud Engineer, or DevOps Engineer interview**, focus on the following areas.

## AWS

* VPC
* Subnets
* CIDR
* Route Tables
* Internet Gateway
* NAT Gateway
* Security Groups
* Network ACLs
* IAM
* EC2
* Auto Scaling
* Load Balancers
* S3
* RDS
* EKS
* CloudWatch
* Route 53

## Kubernetes

* Pods
* Deployments
* ReplicaSets
* Services
* Ingress
* ConfigMaps
* Secrets
* Persistent Volumes
* Persistent Volume Claims
* Readiness Probes
* Liveness Probes
* Resource Requests
* Resource Limits
* HPA
* Node Autoscaling
* Managed Nodes
* Self-Managed Nodes
* Kubernetes Upgrades
* Kubernetes Networking
* DNS
* Troubleshooting

## Terraform

* Terraform State
* Remote Backend
* State Locking
* Terraform Plan
* Terraform Apply
* Terraform Destroy
* Variables
* Outputs
* Modules
* Workspaces
* Infrastructure Drift
* State Security
* Collaboration
* CI/CD Integration

---

# Scenario-Based Questions to Prepare

In addition to the questions asked during this interview, prepare for practical scenarios such as:

### Kubernetes

* What happens when a Kubernetes Pod is stuck in `Pending`?
* How would you troubleshoot `CrashLoopBackOff`?
* How would you troubleshoot `ImagePullBackOff`?
* How would you perform a Kubernetes upgrade safely?
* What checks would you perform before upgrading EKS?
* What checks would you perform after upgrading EKS?
* How would you troubleshoot Kubernetes DNS?
* How would you troubleshoot a Service that is not reachable?
* How would you troubleshoot an Ingress returning `503`?
* How would you handle insufficient node capacity?

### AWS

* What happens if a route table is configured incorrectly?
* How would you troubleshoot connectivity between subnets?
* How does traffic move from a private subnet to the internet?
* What is the difference between an Internet Gateway and NAT Gateway?
* How would you design a highly available VPC?
* How would you secure an AWS workload?
* How would you troubleshoot an EC2 connectivity issue?

### Terraform

* How would you handle Terraform state conflicts?
* How would you recover Terraform state?
* How would you secure Terraform state?
* How would you prevent unauthorized infrastructure changes?
* What happens if two engineers run `terraform apply` simultaneously?
* How would you detect infrastructure drift?
* How would you manage Terraform across multiple environments?

---

# How to Answer Experience-Based Questions

For practical interview questions, use a structured approach.

## STAR Method

```text
Situation
    ↓
Task
    ↓
Action
    ↓
Result
```

For technical troubleshooting, use:

```text
Problem
    ↓
Investigation
    ↓
Root Cause
    ↓
Solution
    ↓
Validation
    ↓
Prevention
```

For architecture questions, use:

```text
Requirement
    ↓
Design
    ↓
Technology Choice
    ↓
Implementation
    ↓
Security
    ↓
Scalability
    ↓
Monitoring
    ↓
Cost Optimization
```

This makes the answer stronger than simply listing commands.

---

# What Interviewers Are Really Evaluating

Technical interviews for AWS/DevOps roles are not only about memorizing definitions.

Interviewers are often evaluating whether you can:

### 1. Understand Infrastructure

Can you explain how AWS networking, compute, storage, and security work together?

### 2. Troubleshoot Problems

Can you move from:

```text
Symptom
   ↓
Investigation
   ↓
Root Cause
   ↓
Solution
```

instead of guessing?

### 3. Explain Your Decisions

Can you explain:

> Why did you choose this architecture?

rather than simply:

> This is what I configured.

### 4. Handle Production Risk

Can you understand:

* Blast radius
* High availability
* Disaster recovery
* Security
* Monitoring
* Cost
* Change management

### 5. Demonstrate Real Experience

If your resume says you worked with Kubernetes, AWS, or Terraform, expect the interviewer to go several levels deeper.

---

# Final Takeaway

The biggest lesson from this interview is:

> **Knowing commands is not enough. You need to understand why you are using them and how they fit into a production environment.**

For an AWS Engineer or DevOps role, be prepared to explain:

```text
What did you implement?
        ↓
Why did you implement it?
        ↓
How did you implement it?
        ↓
What problem did you face?
        ↓
How did you troubleshoot it?
        ↓
What was the root cause?
        ↓
What solution did you implement?
        ↓
How did you validate the solution?
        ↓
How did you prevent the problem from happening again?
```

There is a major difference between:

> **"I have studied Kubernetes."**

and:

> **"I have actually operated Kubernetes."**

The same applies to AWS and Terraform.

The strongest interview preparation is therefore not just memorizing interview questions.

You should be able to explain your:

* Real project architecture
* Technical decisions
* AWS infrastructure
* Kubernetes implementation
* Terraform workflow
* Troubleshooting approach
* Production challenges
* Security practices
* Scalability decisions
* Cost considerations
* Monitoring strategy

---

# Interview Preparation Checklist

Before attending an AWS/DevOps interview, make sure you can confidently answer:

* [ ] Can I explain my project architecture?
* [ ] Can I explain every AWS service on my resume?
* [ ] Can I explain my VPC and subnet design?
* [ ] Can I explain CIDR ranges?
* [ ] Can I explain route tables?
* [ ] Can I explain public vs private subnets?
* [ ] Can I explain NAT Gateway vs Internet Gateway?
* [ ] Can I explain EKS architecture?
* [ ] Can I explain managed vs self-managed nodes?
* [ ] Can I explain Kubernetes upgrades?
* [ ] Can I explain post-upgrade validation?
* [ ] Can I explain Kubernetes autoscaling?
* [ ] Can I explain HPA?
* [ ] Can I explain node autoscaling?
* [ ] Can I explain Terraform state?
* [ ] Can I explain remote state?
* [ ] Can I explain state locking?
* [ ] Can I explain Terraform state security?
* [ ] Can I explain a real production challenge?
* [ ] Can I explain how I troubleshoot incidents?

---

# Conclusion

This interview was a good reminder that AWS Engineer interviews increasingly focus on **practical infrastructure knowledge, troubleshooting, and real-world problem solving**.

The important areas are not isolated technologies.

You need to understand how they work together:

```text
AWS
 ↓
Networking
 ↓
Compute
 ↓
Kubernetes
 ↓
Application Deployment
 ↓
Terraform
 ↓
Automation
 ↓
Monitoring
 ↓
Troubleshooting
```

A strong AWS/DevOps engineer should be able to understand the **complete infrastructure lifecycle**:

```text
Design
  ↓
Provision
  ↓
Configure
  ↓
Deploy
  ↓
Monitor
  ↓
Troubleshoot
  ↓
Scale
  ↓
Secure
  ↓
Optimize
  ↓
Maintain
```

The goal should not be to memorize 20 interview answers.

The goal is to understand the underlying concepts well enough to explain **what you did, why you did it, how you did it, what went wrong, and how you fixed it.**

---

## Interview Details

**Company:** Infosys
**Role:** AWS Engineer
**Duration:** 38 Minutes
**Primary Topics:** AWS | Kubernetes | Terraform | Networking | Infrastructure | Troubleshooting

---

## Topics Covered

```text
AWS
Kubernetes
Amazon EKS
AWS Networking
CIDR
Subnets
Route Tables
Kubernetes Upgrades
Managed Nodes
Self-Managed Nodes
Kubernetes Autoscaling
Terraform
Terraform State
Remote State
State Locking
Infrastructure Security
Troubleshooting
Project Experience
```

---

**End of Interview Experience**

