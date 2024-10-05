pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')  // Assumes you have set up DockerHub credentials in Jenkins
    }

    stages {
        stage('Checkout the code from GitHub') {
            steps {
                git url: 'https://github.com/Raju9934/Bankproject2.git'
                echo 'GitHub repository checked out'
            }
        }

        stage('Compile the Code with Raju') {
            steps {
                echo 'Starting compilation...'
                sh 'mvn compile'
            }
        }

        stage('Run Unit Tests with Raju') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Code Quality Check (QA) with Raju') {
            steps {
                echo 'Running code quality checks...'
                sh 'mvn checkstyle:checkstyle'
            }
        }

        stage('Package the Application with Raju') {
            steps {
                echo 'Packaging the application...'
                sh 'mvn package'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t myimg .'
            }
        }

        stage('Push Docker Image to DockerHub') {
            steps {
                echo 'Pushing Docker image to DockerHub...'
                sh 'docker tag myimg 2024dock/myimg:tagname'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push 2024dock/myimg:tagname'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'
                sh 'docker run -dt -p 8091:8091 --name c001 myimg'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed'
        }
        success {
            echo 'Pipeline executed successfully'
        }
        failure {
            echo 'Pipeline failed. Please check the logs for details.'
        }
    }
}
