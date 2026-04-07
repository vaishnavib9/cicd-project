CI/CD Pipeline Using Jenkins, Docker & Kubernetes

Objective:
To automate the process of building, packaging, and deploying an application using a CI/CD pipeline.

Architecture Overview:
Developer → GitHub → Jenkins → Docker → Docker Hub → Kubernetes → Application

Tools & Technologies Used:
- GitHub – Source code repository
- Jenkins – Continuous Integration tool
- Docker – Containerization platform
- Docker Hub – Image repository
- Kubernetes – Container orchestration
- Linux (Ubuntu) – Deployment environment

Workflow Explanation:

Step 1: Code Commit
Developer pushes code to GitHub repository.

Step 2: CI – Jenkins
Jenkins builds the application and Docker image.

Step 3: Docker Push
Image is pushed to Docker Hub.

Step 4: CD – Kubernetes
Kubernetes deploys the latest image.

Jenkins Pipeline Script:

pipeline {
 agent any
 stages {
  stage('Clone Code') {
   steps {
    git branch: 'main', url: 'https://github.com/vaishnavib9/cicd-project.git'
   }
  }
  stage('Build Docker Image') {
   steps {
    sh 'docker build -t train-app .'
   }
  }
  stage('Push to Docker Hub') {
   steps {
    sh 'docker tag train-app vaishnavib98/train-app'
    sh 'docker push vaishnavib98/train-app'
   }
  }
  stage('Deploy to Kubernetes') {
   steps {
    sh 'kubectl set image deployment/train-app train-app=vaishnavib98/train-app'
   }
  }
 }
}

Conclusion:
This project demonstrates a complete CI/CD pipeline using Jenkins, Docker, and Kubernetes.