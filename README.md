# AWS Blue-Green & Canary Deployment Architecture

## 📌 Project Overview
This project demonstrates the implementation of **Zero-Downtime Deployment Strategies (Blue-Green & Canary)** on AWS using core infrastructure services. It features secure SSL/TLS communication via AWS Certificate Manager (ACM), custom DNS routing via Route 53, and traffic distribution using Application Load Balancer (ALB).

---

## 📐 Architecture Diagram
![AWS Architecture](./architecture-diagram.png)

---

## 🛠️ AWS Services & Technologies Used
* **DNS & SSL/TLS:** AWS Route 53, AWS Certificate Manager (ACM)
* **Load Balancing:** Application Load Balancer (ALB), Target Groups (Blue & Green)
* **Compute & Auto-Scaling:** EC2, Launch Templates, Auto Scaling Groups (ASG)
* **Networking & Security:** VPC, Public/Private Subnets, Internet Gateway, Route Tables, Security Groups
* **Storage & Recovery:** EBS Volumes (Attach/Detach), EBS Snapshots, Custom AMIs
* **Web Server:** Nginx / Apache (`httpd`)

---

## 🚀 Key Learning & Implementation Steps

### 1. Networking & Security Setup
* Configured custom VPC with Multi-AZ Subnets (1a & 1b) and Internet Gateway.
* Set up Security Groups allowing HTTP (80) & HTTPS (443) traffic.

### 2. Domain & SSL/TLS Setup
* Configured Hosted Zone in **Route 53**.
* Requested a Public Wildcard Certificate in **AWS Certificate Manager (ACM)** and validated DNS records.
* Attached the HTTPS (443) Listener on ALB backed by the ACM SSL Certificate.

### 3. Application Versioning (Blue vs. Green)
* **Blue Environment (v1):** Launched Server-1 & Server-2 attached to `Blue-TG`.
* **Green Environment (v2):** Launched Server-3 & Server-4 attached to `Green-TG`.
* Configured `/index.html` health checks with HTTP 200 responses.

### 4. Deployment Strategies Executed
* **Blue-Green Deployment:** Re-routed 100% traffic from `Blue-TG` (0%) to `Green-TG` (100%) at the ALB listener level with zero downtime.
* **Canary Testing:** Configured Weighted Target Groups (e.g., 90% Blue / 10% Green) to validate Version 2 with real users before full rollout.

### 5. Storage & Disaster Recovery Practices
* Created EBS Snapshots and restored new Volumes across EC2 instances.
* Tested Cross-Instance volume attaching/detaching and custom AMI creation.

---

## 📸 Screenshots & Proof of Work
*(Add your AWS console screenshots here)*
* SSL Certificate Validation in ACM
* ALB Listener Rules (Weighted Target Groups)
* Version 1 (Blue) vs Version 2 (Green) browser outputs
