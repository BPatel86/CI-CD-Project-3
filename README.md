# CI/CD Deployment with Jenkins, Docker, and Tomcat on AWS

## 📘 Overview

This project sets up a simple but effective CI/CD pipeline using **Jenkins**, **Docker**, and **Apache Tomcat** on **AWS EC2** instances. The goal is to automate the entire software delivery process — from source code commit to application deployment in a Dockerized Tomcat container.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/1602326a-94fc-4aa4-80ed-b55eca7db634" />

---

## 🏗️ Architecture

- **EC2 Instance 1 (Jenkins Server)**  
  - Jenkins installed with required plugins (SSH, Maven)
  - Builds the Java application using Maven
  - Sends `.war` file to Docker host and runs deployment commands via SSH

- **EC2 Instance 2 (Docker Host)**  
  - Docker installed and configured
  - Hosts a custom Tomcat container built from a Dockerfile
  - Runs the container serving the deployed application

---

## 🔄 Workflow

1. **Code Push**  
   Developer pushes code to GitHub repository (`main` branch).

2. **Jenkins Build**  
   Jenkins polls GitHub, triggers Maven to build the `.war` file.

3. **Artifact Transfer**  
   Jenkins sends the generated `.war` file to the Docker host using SSH.

4. **Docker Deployment**  
   Jenkins triggers remote Docker commands to:
   - Remove old containers/images
   - Build a new image from Dockerfile
   - Start a new container with the updated application

5. **Access Web App**  
   The Java application is available at:  http://<Docker_Host_Public_IP>:8090/webapp

**New Image and Container created on a Docker host through Jenkins Jobs.**
Verified through the following command:
    docker ps
    docker images


