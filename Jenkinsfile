pipeline {
    agent any

    stages {
        stage('Checkout Code from GitHub') {
            steps {
                git url: 'https://github.com/Raju9934/Bankproject2.git'
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
        
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'
                sh 'docker build -t myimg .'
            }
        }
        
        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container'
                sh 'docker run -dt -p 8091:8091 --name c001 myimg'
            }
        }
        
        stage('Clean and Install Maven') {
            steps {
                echo 'Cleaning and installing Maven'
                sh 'mvn clean install'
            }
        }
        
        stage('Build Docker Image for Docker Hub') {
            steps {
                echo 'Building Docker image for Docker Hub'
                sh 'docker build -t 2024dock/myimg:v1 .'
            }
        }
        
        stage('Docker Login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push 2024dock/myimg:v1' // corrected the image name here
                    }
                }
            }
        }
    }
}
