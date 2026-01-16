---

# 🚀 AWS CloudFormation – VPC Networking & Application Layer Deployment using IaC

## 📌 Project Overview

This project demonstrates the use of **AWS CloudFormation** to deploy infrastructure without using management console. The infrastructure is divided into two independent layers

1. **Networking Layer** – Creates the VPC and networking components
2. **Application Layer** – Deploys an EC2-based web application and referencing the networking layer

The application layer is later **updated to allow SSH access** and successfully serves a web page, proving end-to-end deployment.

---

## 🏗️ Architecture Overview

### 🔹 Networking Layer (Stack 1)

* Virtual Private Cloud (VPC)
* Public Subnet
* Internet Gateway
* Route Table with Internet access

### 🔹 Application Layer (Stack 2)

* EC2 Instance launched in the public subnet
* Security Group attached to EC2
* Web server installed using UserData
* Cross-layer references to VPC and Subnet

---

## 🔁 Cross-layer Design

* The **Networking layer** exports values such as:

  * VPC ID
  * Public Subnet ID to Application layer
* The **Application layer** imports these values using:

  * `Fn::ImportValue`
* This ensures **modularity, reusability, and clean separation of concerns**

---
After deploying both layers successfully, the EC2 instance was accessed using its public DNS.

🎯 Application Output

When accessed via browser, the following message is displayed:

“Congratulations, you have successfully launched the AWS CloudFormation sample.”

## 🔐 Security Group Update (SSH Access)

The Application Layer was updated to include an inbound rule:

* **Protocol:** TCP
* **Port:** 22
* **Source:** Trusted IP / `0.0.0.0/0` (for lab/testing)

SSH access was enabled on the EC2 security group to allow secure remote administration, troubleshooting, and validation of the CloudFormation-deployed application instance.

---


This confirms:

* EC2 instance launched successfully
* Networking configuration works correctly
* Internet Gateway and routing are properly configured
* Application layer is fully functional

📸 *Screenshot evidence is included in the repository for validation.*

---


```

---

## ⚠️ Challenges Faced

### Problem

The application layer initially failed due to missing VPC and subnet references.

### Solution

* Used CloudFormation **Outputs and Exports** in the networking stack
* Imported values in the application stack using `Fn::ImportValue`

---



