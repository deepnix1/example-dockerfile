# CI/CD Pipeline with Jenkins 🛠️

## Overview
This repository contains a Jenkins pipeline for building, testing, analyzing, and deploying a Java-based application using Docker and SonarQube.

## Pipeline Stages 🚀
1. **Git Checkout** - Clones the repository  
2. **Compile** - Builds the Java application using Maven  
3. **OWASP Security Check** - Runs OWASP Dependency Check  
4. **Build Application** - Compiles and packages the application  
5. **Build & Push Docker Image** - Creates and uploads the Docker image to a registry  
6. **SonarQube Analysis** - Performs code analysis with SonarQube  
7. **Trigger CD Pipeline** - Deploys the application  

## How to Run Locally 🏃
1. Install **Jenkins**, **Docker**, **Maven**, and **SonarQube**  
2. Add credentials for **DockerHub** and **SonarQube**  
3. Configure **SonarQube URL & Token** in Jenkins  
4. Run the pipeline from Jenkins UI  

## Pipeline Configuration 🔧
The Jenkins pipeline is defined in the `Jenkinsfile`:

```groovy
pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven'
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
        SONAR_AUTH_TOKEN = credentials('sonarqube-token')
        SONAR_URL = '<IP_ADRESS:9000>'
    }

    stages {
        stage('Git Checkout') { ... }
        stage('Compile') { ... }
        stage('OWASP check') { ... }
        stage('Build application') { ... }
        stage('Build & Push Docker Image') { ... }
        stage('SonarQube Analysis') { ... }
        stage('Trigger CD pipeline') { ... }
    }
}
