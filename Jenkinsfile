pipeline {
    agent any

    stages {
        stage('Checkout Code from GitHub') {
            steps {
                git url: 'https://github.com/Raju9934/java-project1.git'
                echo 'Checked out code from GitHub'
            }
        }
        
        stage('Compile Code') {
            steps {
                echo 'Starting compilation'
                sh 'mvn compile'
            }
        }
        
        stage('Run Tests') {
            steps {
                echo 'Running tests'
                sh 'mvn test'
            }
        }
        
        stage('Quality Assurance') {
            steps {
                echo 'Running Checkstyle'
                sh 'mvn checkstyle:checkstyle'
            }
        }
        
        stage('Package Application') {
            steps {
                echo 'Packaging application'
                sh 'mvn package'
            }
        }

        stage('Clean and Install Maven') {
            steps {
                echo 'Cleaning and installing Maven'
                sh 'mvn clean install'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'
                sh 'docker build -t java-project:1.0 .'
            }
        }
        
        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container'
                sh 'docker run -dt -p 8091:8091  java-project:1.0 '
            }
        }
        
        stage('create tag  Image for Docker Hub') {
            steps {
                echo 'tagging image'
                sh 'docker tag java-project:1.0  2024dock/java-project:1.0'
            }
        }
        
        stage('Docker Login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push 2024dock/java-project:1.0  ' // corrected the image name here
                    }
                }
            }
        }
    }
}
