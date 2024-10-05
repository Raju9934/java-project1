pipeline {
    agent any
    stages {
        stage('Checkout the code from GitHub') {
            steps {
                git url: 'https://github.com/Raju9934/Bankproject2.git'
                echo 'Checked out the GitHub repository'
            }
        }
        stage('Compile Code') {
            steps {
                echo 'Starting code compilation'
                sh 'mvn compile'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests'
                sh 'mvn test'
            }
        }
        stage('Code Quality Check') {
            steps {
                echo 'Running QA checks with Checkstyle'
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
        stage('Docker Login') {
            steps {
                echo 'Logging in to Docker Hub'
                sh 'echo "9934263946" | docker login -u "dock2024" --password-stdin'
            }
        }
        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    echo 'Tagging Docker image'
                    sh 'docker tag myimg dock2024/myimg:latest'
                    
                    echo 'Pushing Docker image to Docker Hub'
                    sh 'docker push dock2024/myimg:latest'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container'
                sh 'docker run -dt -p 8091:8091 --name c001 dock2024/myimg:latest'
            }
        }
    }
}
