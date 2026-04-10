# 🔄 Auto-Healing Infrastructure on AWS

## 📌 Project Overview

This project demonstrates a **self-healing infrastructure** on AWS where failed EC2 instances are automatically detected and replaced using **Auto Scaling and CloudWatch**.

👉 The system ensures **high availability and fault tolerance** without manual intervention.

---

## 🧱 Architecture

```id="arch1"
User Traffic
     ↓
Application Load Balancer (ALB)
     ↓
Auto Scaling Group (EC2 Instances)
     ↓
CloudWatch (Health Monitoring)
     ↓
Auto Scaling (Replace Unhealthy Instance)
```

<p align="center">
<svg width="800" height="300" xmlns="http://www.w3.org/2000/svg">

  <!-- User -->

  <rect x="20" y="120" width="100" height="60" rx="10" fill="#4CAF50"/>
  <text x="70" y="155" fill="white" font-size="12" text-anchor="middle">User</text>

  <!-- ALB -->

  <rect x="180" y="110" width="140" height="80" rx="10" fill="#2196F3"/>
  <text x="250" y="150" fill="white" font-size="12" text-anchor="middle">Load Balancer</text>

  <!-- EC2 Instances -->

  <rect x="380" y="60" width="120" height="60" rx="10" fill="#FF9900"/>
  <text x="440" y="95" fill="white" font-size="12" text-anchor="middle">EC2 #1</text>

  <rect x="380" y="150" width="120" height="60" rx="10" fill="#FF9900"/>
  <text x="440" y="185" fill="white" font-size="12" text-anchor="middle">EC2 #2</text>

  <!-- Auto Scaling -->

  <rect x="560" y="100" width="160" height="80" rx="10" fill="#9C27B0"/>
  <text x="640" y="145" fill="white" font-size="12" text-anchor="middle">Auto Scaling</text>

  <!-- Arrows -->

  <line x1="120" y1="150" x2="180" y2="150" stroke="#00F7FF" stroke-width="2"/>
  <line x1="320" y1="150" x2="380" y2="90" stroke="#00F7FF" stroke-width="2"/>
  <line x1="320" y1="150" x2="380" y2="180" stroke="#00F7FF" stroke-width="2"/>
  <line x1="500" y1="90" x2="560" y2="130" stroke="#00F7FF" stroke-width="2"/>
  <line x1="500" y1="180" x2="560" y2="150" stroke="#00F7FF" stroke-width="2"/>

</svg>
</p>

<p align="center">
High Availability + Self-Healing using Auto Scaling
</p>


---

## ⚙️ Tech Stack

* ☁️ AWS EC2 (Compute)
* ⚖️ Auto Scaling Group (High Availability)
* 🌐 Application Load Balancer (Traffic Distribution)
* 📊 CloudWatch (Monitoring & Alerts)
* ⚡ AWS Lambda (Optional automation)

---

## 🚀 Features

* ✅ Automatic instance replacement on failure
* ✅ High availability using multiple EC2 instances
* ✅ Load balancing across instances
* ✅ Health checks with CloudWatch
* ✅ Zero downtime architecture

---

## 🛠️ Setup & Implementation

### 1️⃣ Launch EC2 Instance (Base Template)

* Amazon Linux 2
* Install Apache

```bash id="cmd1"
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

---

### 2️⃣ Create AMI

* Go to EC2 → Actions → Create Image
  👉 This will be used by Auto Scaling

---

### 3️⃣ Create Launch Template

* Select created AMI
* Instance type: t2.micro
* Add Security Group:

  * 80 (HTTP)
  * 22 (SSH)

---

### 4️⃣ Create Auto Scaling Group

* Min: 2
* Desired: 2
* Max: 3

👉 Ensures at least 2 instances always running

---

### 5️⃣ Attach Load Balancer

* Create **Application Load Balancer**
* Add target group
* Register Auto Scaling instances

---

### 6️⃣ Enable Health Checks

* Use:

  * EC2 health check
  * ALB health check

👉 If instance fails → Auto Scaling replaces it

---

## 🔁 Auto-Healing Workflow

1. Application runs on multiple EC2 instances
2. CloudWatch monitors instance health
3. If instance fails → marked unhealthy
4. Auto Scaling terminates instance
5. New instance launched automatically
6. Load Balancer routes traffic to healthy instances

---

## 🧪 Testing the Auto-Healing

### Simulate Failure:

```bash id="cmd2"
sudo systemctl stop httpd
```

OR terminate instance manually

👉 Result:

* Instance becomes unhealthy
* Auto Scaling launches new instance
* Traffic continues without downtime

---

## 🎯 Key Learnings

* High availability architecture
* Fault tolerance in cloud systems
* Auto Scaling concepts
* Load balancing strategies
* Monitoring using CloudWatch

---

## 📊 Outcome

* 🔄 Achieved self-healing infrastructure
* 🚀 Improved system reliability
* ⚡ Eliminated manual recovery effort
* 💼 Built production-like resilient system

---

## 🌐 Connect With Me

* LinkedIn: https://linkedin.com/in/farish98

---
