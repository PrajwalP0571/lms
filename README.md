# Learning Management System
![Multi-tire Application project Architect Diagram](https://github.com/user-attachments/assets/f7224123-9094-4eb0-9307-372c148d4eba)

## REACT JS - Presentation tier
## NODE JS - Application tier
## POSTGRES - Data tier

Introduction
"In this project, I designed and deployed a Learning Management System (LMS) following a multi-tier architecture on AWS. The project included setting up a development environment, building and deploying backend and frontend services, and performing static code analysis to ensure high code quality. The LMS uses PostgreSQL for the database, Node.js for the backend, and React.js for the frontend. I also integrated SonarQube for continuous code quality monitoring. Here's how I implemented the project step-by-step."

Phase 1: Architecture Design and Setup

1. Multi-Tier Architecture:

Implemented three-tier architecture:
Frontend Layer: React.js for UI/UX.
Application Layer: Node.js for business logic.
Database Layer: PostgreSQL for data storage.

2. AWS Infrastructure Setup:

Provisioned a t2.medium EC2 instance (4 GB RAM, 2 vCPUs, 8 GB storage) on AWS.
Configured Security Groups for required ports:
22: SSH for access.
5432: PostgreSQL database.
8080: Node.js backend.
80: React.js frontend hosted via Nginx.
Phase 2: Database Setup (PostgreSQL)

1. PostgreSQL Installation:

Installed PostgreSQL and set the password for the database user.
Configured connection details for backend API:
bash
Copy code
DATABASE_URL=postgresql://postgres:password@localhost:5432/postgres

Phase 3: Backend Development (Node.js)

1. Node.js Installation:

Installed Node.js v16 and npm package manager.

2. API Development:

Cloned backend code from the repository:
bash
Copy code
git clone -b dev https://github.com/ravi2krishna/lms.git
cd ~/lms/api
Configured database connection in .env file.

3. Database Migration and Schema Setup:

Used Prisma ORM for database migrations and schema definition:
bash
Copy code
npm install
npx prisma generate
npx prisma db push

4. Backend Build and Deployment:

Built and verified the API locally:
bash
Copy code
npm run build
node build/index.js
Used PM2 for process management and backend deployment:
bash
Copy code
sudo npm install -g pm2
pm2 start build/index.js

Phase 4: Frontend Development (React.js)

1. Frontend Setup:

Cloned the frontend code:
bash
Copy code
cd ~/lms/webapp
Configured backend URL in .env file:
arduino
Copy code
VITE_API_URL=http://<public-ip>:8080/api

2. Frontend Build:

Built the React application to generate static files:
bash
Copy code
npm install
npm run build

3. Web Server Configuration (Nginx):

Installed Nginx to host the React app:
bash
Copy code
sudo apt -y install nginx
sudo cp -r ~/lms/webapp/dist/* /var/www/html
Verified deployment by accessing the LMS via public IP:
vbnet
Copy code
http://<public-ip>

Phase 5: Code Quality and Static Analysis (SonarQube)
1. SonarQube Setup:

Deployed SonarQube as a Docker container on AWS (t2.medium instance):
bash
Copy code
sudo docker run -dt --name sonarqube --restart=always -p 9000:9000 sonarqube
Configured SonarQube with default credentials (admin/admin) and connected it to the LMS repository for analysis.

2. Static Code Analysis:

Used SonarQube’s scanner tool for analyzing the LMS codebase:
bash
Copy code
sudo docker run --rm -e SONAR_HOST_URL="http://<ip>:9000" -e SONAR_LOGIN="<token>" -v ".:/usr/src" sonarsource/sonar-scanner-cli:5.0 -Dsonar.projectKey=lms
Identified and fixed issues like:
Unused variables and methods.
Security vulnerabilities (e.g., SQL injection risks).
Code style violations.

Phase 6: Testing and Deployment
1. Backend Testing:

Verified API endpoints using curl and browser:
bash
Copy code
curl http://localhost:8080/api
Response:
json
Copy code
{"message":"success","mode":"production"}

2. Frontend Testing:

Verified the web application using the public IP of the EC2 instance:
vbnet
Copy code
http://<public-ip>

3. Final Deployment:

Ensured high availability and scalability by using PM2 for backend monitoring and Nginx for frontend hosting.
Key Features and Benefits
Scalable Multi-Tier Architecture:
Separated frontend, backend, and database layers for scalability and maintenance.
CI/CD Pipeline Compatibility:
Leveraged Docker and SonarQube for seamless integration into DevOps workflows.
Improved Code Quality:
Used static code analysis to ensure security, performance, and maintainability.
High Availability:
Deployed PM2 for automatic restarts and monitoring, reducing downtime.
AWS Infrastructure Utilization:
Leveraged AWS EC2 for flexibility and scalability.

Conclusion
"This project demonstrates my expertise in cloud infrastructure, DevOps practices, containerization, and multi-tier application development. By integrating tools like Docker and SonarQube, I ensured code quality, modularization, and scalability, aligning with industry best practices."
