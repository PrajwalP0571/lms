# Learning Management System
![Multi-tire Application project Architect Diagram](https://github.com/user-attachments/assets/f7224123-9094-4eb0-9307-372c148d4eba)

## REACT JS - Presentation tier
## NODE JS - Application tier
## POSTGRES - Data tier

# 🏫 LMS Project – Full Stack Build on AWS & Azure  

## 📅 Date: 11 Oct 2024  

![AWS](https://img.shields.io/badge/AWS-t2.medium-orange?style=flat&logo=amazonaws)  
![Azure](https://img.shields.io/badge/Azure-B2S-blue?style=flat&logo=microsoftazure)  
![PostgreSQL](https://img.shields.io/badge/Database-Postgres-blue?style=flat&logo=postgresql)  
![Node.js](https://img.shields.io/badge/Backend-Node.js-green?style=flat&logo=node.js)  
![React](https://img.shields.io/badge/Frontend-React-blue?style=flat&logo=react)  

---

## 📌 **Project Overview**  
This project sets up a **Learning Management System (LMS)** as a multi-tier application using AWS and Azure. The LMS consists of the following components:

1. **Database Layer** – PostgreSQL database for storing user data and course details  
2. **Application Layer** – Node.js backend to handle business logic and API calls  
3. **Frontend Layer** – React.js for a responsive and dynamic user interface  
4. **Web Server** – NGINX to serve the frontend and handle client requests  

The infrastructure is designed to be scalable, secure, and easily manageable. This guide includes detailed steps for deploying each layer, setting up security, and troubleshooting common issues.

---

## 🏢 **Infrastructure Setup**  

| Tier              | Port | Service       | Description                     |
|-------------------|------|---------------|---------------------------------|
| **SSH**           | 22   | Login          | Secure Shell Access             |
| **Database Tier** | 5432 | PostgreSQL     | Storing LMS data               |
| **App Tier**      | 8080 | Node.js         | Business Logic and API         |
| **Frontend Tier** | 80   | React.js (Nginx) | User Interface                 |

---

## 🖥️ **EC2 Instance Requirements**  
To host the LMS, create a virtual machine with the following specifications:

### ✅ **AWS:**  
- Instance Type: `t2.medium`  
- CPU: **2 vCPUs**  
- RAM: **4 GB**  
- Storage: **8 GB**  

### ✅ **Azure:**  
- Instance Type: `B2S`  
- CPU: **2 vCPUs**  
- RAM: **4 GB**  
- Storage: **8 GB**  

---

## 🚀 **Setup Instructions**  

### **1️⃣ Step 1: Setup PostgreSQL Database**  
The LMS will store data such as user information, course details, and progress in a PostgreSQL database.

#### ✅ Install PostgreSQL:
1. Update the system packages:
```bash
sudo apt update

2. Install PostgreSQL:
```bash
sudo apt install postgresql postgresql-contrib

3. Start and enable the PostgreSQL service:
```bash
sudo systemctl start postgresql
sudo systemctl enable PostgreSQL

4. Verify PostgreSQL is running:
```bash
sudo ss -ntpl






