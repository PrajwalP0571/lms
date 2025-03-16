# Learning Management System
![Multi-Tier Application Deployment](https://github.com/user-attachments/assets/f0eae0c7-f050-4293-b149-5c81c50164a0) width="200"

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
```

2. Install PostgreSQL:
```bash
sudo apt install postgresql postgresql-contrib
```

3. Start and enable the PostgreSQL service:
```bash
sudo systemctl start postgresql
sudo systemctl enable PostgreSQL
```

4. Verify PostgreSQL is running:
```bash
sudo ss -ntpl
```

### ✅ Set up PostgreSQL password:
Switch to the postgres user:
```bash
sudo su - postgres
```

Open the PostgreSQL command-line interface:
```bash
psql
```

Set a password for the postgres user:
```bash
sql
\password
```

Exit the PostgreSQL shell:
```bash
sql
Copy code
\q
```

### 2️⃣ Step 2: Setup Application Layer
The application layer (API) is built using Node.js and manages business logic and client interactions.

### ✅ Install Node.js (Version 16):

Add the Node.js repository:
```bash
curl -sL https://deb.nodesource.com/setup_16.x | sudo bash -

Install Node.js:
```bash
sudo apt-get install -y nodejs
```

Verify the installation:
```bash
node -v
npm -v
```

### 3️⃣ Step 3: Build LMS API
The backend is built using Node.js and connects to the PostgreSQL database.

### ✅ Clone the LMS repository:
Switch to the home directory:
```bash
cd ~
```

Clone the LMS source code:
```bash
git clone -b dev https://github.com/PrajwalP0571/lms.git
```

### ✅ Configure the API:
Create a .env file in the api directory:
```bash
cd ~/lms/api
vi .env
```

Add the following configuration:
env
```bash
MODE=dev
PORT=8080
DATABASE_URL=postgresql://postgres:<your-password>@localhost:5432/postgres
```

### ✅ Install dependencies:
```bash
npm install
```

### ✅ Generate Prisma client and push DB schema:
Generate the database schema:
```bash
sudo npx prisma generate
```

Push the schema to PostgreSQL:
```bash
sudo npx prisma db push
```

Verify the tables in PostgreSQL:
```bash
sudo su - postgres
psql
\dt
\q
```

### ✅ Build LMS API:
```bash
npm run build
```

### ✅ Start LMS API using PM2:
Install PM2 (process manager):
```bash
sudo npm install -g pm2
```

Start the API:
```bash
pm2 start build/index.js
```

Check if the API is running:
```bash
pm2 status
```

Test the API locally:
```bash
curl http://localhost:8080/api
```

Expected Output:

json
{"message":"success","mode":"dev"}

### 4️⃣ Step 4: Build LMS Frontend
The frontend is built using React.js.

### ✅ Configure the frontend:
Create a .env file in the webapp directory:
```bash
cd ~/lms/webapp
vi .env
```

Add the following:
'''bash
env
VITE_API_URL=http://public-ip:8080/api
```

### ✅ Build frontend:
```bash
npm install
npm run build
```

### 5️⃣ Step 5: Setup NGINX Web Server
Install NGINX:
```bash
sudo apt install nginx
```

Copy the frontend build to the NGINX root:
```bash
sudo cp -r ~/lms/webapp/dist/* /var/www/html
```

Restart NGINX:
```bash
sudo systemctl restart nginx
```
Test frontend: 👉 http://public-ip

🧪 Testing and Troubleshooting
### ✅ Database:
Stop and start PostgreSQL:
```bash
sudo systemctl stop postgresql
sudo systemctl start PostgreSQL
```

### ✅ API:
Restart API using PM2:
```bash
pm2 restart 0
```

Test API:
```bash
curl http://localhost:8080/api
```

### ✅ Frontend:
Restart NGINX:
```bash
sudo systemctl restart nginx
```

Test frontend: 👉 http://public-ip
📸 Screenshots
✅ API Running:

✅ Frontend Running:

🔥 Deployment Status
✅ PostgreSQL – Running
✅ Node.js API – Running
✅ Frontend (React) – Deployed
✅ NGINX – Configured

🎯 Next Steps
✅ Add monitoring with CloudWatch
✅ Set up a CI/CD Pipeline using Jenkins
✅ Implement auto-scaling and load balancing
💡 Author
Prajwal Pawar
📧 prajwal.pawar0571@gmail.com
LinkedIn



