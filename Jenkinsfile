pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven'
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
        SONAR_AUTH_TOKEN = 'squ_6de207690725b7961e5f226fc8b85c3fea39d0b0'
        SONAR_URL = 'http://172.27.80.1:9000'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/deepnix1/example-dockerfile.git'
            }
        }
        
        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
        
        stage('OWASP check') {
            steps {
                dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        } // << Eksik kapanış kapatıldı

        stage('Build application') {
            steps {
                sh 'mvn clean install' // "maven" yerine "mvn" olmalı
            }
        }
        
        stage('Build & Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '8cd03fa9-2f63-40c7-b972-7e14f17b4a8b') {
                        sh "docker build -t shopping:latest -f docker/Dockerfile ."
                        sh "docker tag shopping:latest mustafadall1/shopping:latest"
                        sh "docker push mustafadall1/shopping:latest"
                    }
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('Sonarqube') { // Ensure this matches your Jenkins SonarQube configuration name
                    sh '''
                    $SCANNER_HOME/bin/sonar-scanner \
                      -Dsonar.projectKey=jenkins-sonarqubee \
                      -Dsonar.projectName=jenkins-sonarqubee \
                      -Dsonar.host.url=$SONAR_URL \
                      -Dsonar.login=$SONAR_AUTH_TOKEN \
                      -Dsonar.java.binaries=target/classes
                    '''
                }
            }
        }
        
        
        stage('Trigger CD pipeline') {
            steps {
                script {
                    build job: "CD_Pipeline" , wait: true
                }
            }
        }
    }
}
