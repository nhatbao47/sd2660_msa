pipeline {
    agent any
    stages {
        stage('Build backend') {
            steps {
                echo 'Build backend image'
            }
        }

        stage('Build frontend') {
            steps {
                echo 'Build front image'
            }
        }

        stage('Push backend') {
            steps {
                echo 'Push backend image to ECR'
            }
        }

        stage('Push frontend') {
            steps {
                echo 'Push frontend image to ECR'
            }
        }
    }
}