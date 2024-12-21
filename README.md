![image](https://github.com/user-attachments/assets/00a49ab9-5746-4383-acc6-21624061a967)# Learning Management System

## REACT JS - Presentation tier
## NODE JS - Application tier
## POSTGRES - Data tier

Static Code Analysis
Static code analysis is analyzing source code without actually executing it. 


It involves examining the code for potential issues, vulnerabilities, and adherence to coding standards and best practices. 

Static code analysis can help identify various types of issues, including:

Syntax errors and typos
Unused variables and methods
Code duplication
Security vulnerabilities (e.g., SQL injection, cross-site scripting)
Memory leaks and resource leaks
Performance issues
Conformance to coding standards and style guidelines (e.g., indentation, naming conventions)

By detecting these issues early in the development process, static code analysis helps reduce the likelihood of bugs, security vulnerabilities, and maintenance headaches later on. 

Static code analysis promotes code quality, consistency, and reliability across software projects.

SonarQube
SonarQube is an open source platform developed by SonarSource for continuous inspection of Code Quality



Setting Up SonarQube
SonarQube Requires “t2.medium instance” i.e 4 GB RAM - 2 CPU’s on AWS, with 8 GB as Storage.

SonarQube works on “port 9000”, make sure to add port 9000 as part of your Security Group

https://github.com/jae1choi/sonaqueue-installation-guide





Install Docker
docker
curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh
docker

Install SonarQube
sudo ss -ntpl
sudo docker container run -dt --name sonarqube --restart=always -p 9000:9000 sonarqube
sudo ss -ntpl


Default credentials are 
Username is admin 
Password is admin







LMS Project - Code 
https://github.com/ravi2krishna/lms.git

IMPORTANT Fork Above Project to your Github Accounts

Make sure to change the username here from ravi2krishna to your username

ls
git clone -b dev https://github.com/Maheshalagonda/lms.git
ls
cd ~/lms/webapp
ls
sudo docker run  --rm -e SONAR_HOST_URL="http://35.90.93.22:9000" -e SONAR_LOGIN="sqp_aca3716695f93a33e306b925beb34976caf13502"  -v ".:/usr/src" sonarsource/sonar-scanner-cli:5.0 -Dsonar.projectKey=lms








Multi Tier App Architecture
The three tier architecture is a widely used architectural pattern that divides an application into three interconnected layers: the presentation layer, the application layer and the database layer.
💡 The frontend layer is responsible for displaying the user interface and receiving user input.
💡 The application layer contains the business logic and processes the user input.
💡 Finally, the database layer is responsible for storing and retrieving data used by the application.


Application Stack
An application stack is a set of software programs that include software for the front-end, the back-end and the database.

Most Popular Stacks
https://en.wikipedia.org/wiki/Programming_languages_used_in_most_popular_websites
LMS Application Stack
Database : POSTGRES
Application : NODEJS
Frontend : REACTJS

17 Apr 2024 
LMS Project - BUILD 
Software Build
The term build may refer to the process by which source code is converted into binary code (software artifact)

Any Build Implementation

Source Code Files 
Source code is the list of human-readable instructions that a programmer writes often in a word processing program when he is developing a program.

Metadata File
It is a file that contains information about the project and configuration details used to build the project. 

Binary Code (After Builds)
Build artifacts are files produced by a build.










As LMS App is multi tier, We need Following Rules in Security Group
SSH - 22 - Login
DATABASE TIER [ POSTGRES ] - 5432 - Storing Data
APPLICATION TIER [ NODEJS ] - 8080 - Business Logics
FRONTEND TIER [ REACTJS ] { Hosted Web Server } - 80

LMS Requires “t2.medium instance” i.e 4 GB RAM - 2 CPU’s on AWS, with 8 GB as Storage.

Setup LMS dev Environment 
Setup Database for LMS
Install postgres 

> Goto https://www.postgresql.org/download/linux/ubuntu/
Set Password - postgres 
Commands to set the password for postgres database
sudo su - postgres
psql
\password
\q
exit


Setup App Layer For LMS 
 install Node.js version 16 on your system

node -v
npm -v
curl -sL https://deb.nodesource.com/setup_16.x | sudo bash -
sudo apt-get install -y nodejs
node -v
npm -v







Build API For LMS
Change the directory to api, Then create a .env file in the api folder which is our backend source code, where we would specify the database connection details.

git clone -b dev https://github.com/ravi2krishna/lms.git
cd ~/lms/api
vi .env

MODE=production
PORT=8080
DATABASE_URL=postgresql://postgres:your-password@localhost:5432/postgres




18 Apr 2024 
Build Backend

npm install
cat prisma/migrations/20221110085013_init/migration.sql
sudo npx prisma generate
sudo npx prisma db push
\dt {in postgres}
ls build
npm run build
ls build
sudo ss -ntpl
node build/index.js
ctrl + c
sudo npm install -g pm2
pm2 start build/index.js
sudo ss -ntpl



Locally verify 
curl http://localhost:8080/api


{"message":"success","mode":"production"}

Verify with Browse - http://public-ip:8080/api

Build Frontend For LMS
Change the directory to webapp, Then create a .env file in the webapp folder which is our frontend source code, where we would specify the backend connection details.
cd ~/lms/webapp
vi .env

VITE_API_URL=http://public-ip:8080/api



Run the below commands to build the Application, which will create dist folder, in which our application will be made available
npm install
ls dist
npm run build
ls dist



Setup Nginx Web Server
sudo ss -ntpl
sudo apt -y update
sudo apt -y install nginx
sudo ss -ntpl



Test Web Server
💡 Browse - http://public-ip

💡 If you are the website administrator: You may now add webapp content to the directory DocumentRoot - /var/www/html/

ls /var/www/html
cat /var/www/html/index.nginx-debian.html
sudo rm -rf /var/www/html/*
ls /var/www/html
sudo cp -r ~/lms/webapp/dist/* /var/www/html
ls /var/www/html
ls ~/lms/webapp/dist/





