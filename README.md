# Web Server Automation and CI/CD using Ansible and Jenkins

## Project Overview
This project demonstrates automation of web server setup and deployment using Ansible and Jenkins.  
Ansible is used to configure Nginx and Tomcat servers, and Jenkins is used to automate the build and deployment process.

---

## Tech Stack
- Jenkins (CI/CD)
- Ansible (Automation)
- Apache Tomcat (Application Server)
- Nginx (Web Server)
- Maven (Build Tool)
- Git & GitHub (Version Control)
- Linux

---

## Workflow
1. Ansible roles are used to set up Nginx and Tomcat servers  
2. Initial deployment is done manually for testing  
3. Code is pushed to GitHub  
4. Jenkins triggers build process  
5. Maven builds the application  
6. Jenkins uses Ansible to deploy application to Tomcat  
7. Nginx acts as reverse proxy (if configured)  

---

## Setup Instructions

### Clone Repository
git clone https://github.com/your-username/your-repo.git  
cd your-repo  

### Prerequisites
- Java  
- Maven  
- Jenkins  
- Ansible  
- Tomcat  
- Nginx  
- Git  

### Configure Ansible
- Create roles for:
  - Tomcat setup
  - Nginx setup
- Update inventory file with target server details

### Run Ansible Roles (Initial Setup)
ansible-playbook -i inventory main.yml  

### Manual Deployment (Initial Testing)
mvn clean install  
- Deploy generated .war file manually to Tomcat  

### Jenkins Automation
- Create Jenkins pipeline job  
- Connect GitHub repository  
- Add Jenkinsfile  
- Configure stages:
  - Build using Maven  
  - Deploy using Ansible  

### Access Application
Start Tomcat server:
./startup.sh  

Then open in browser:
http://52.66.73.212:8080/app-name  

Note: Server must be running to access the application.

---

## Results
- Automated server configuration using Ansible  
- Reduced manual deployment effort  
- Implemented CI/CD using Jenkins  

---

## Author
Prakash Reddy  
LinkedIn: https://www.linkedin.com/in/c-prakash-reddy-0307b3256/  
GitHub: https://github.com/PrakashReddy19
