pipeline {
    agent none
    environment {
        REGION = "ap-southeast-1"
        FRONTEND_APP = "frontend"
        BACKEND_APP = "backend"
        ECR_URI = "495016266100.dkr.ecr.ap-southeast-1.amazonaws.com"
        IMAGE_TAG = "${BUILD_NUMBER}"
        GIT_REPO = "https://github.com/nhatbao47/sd2660_msa.git"
        REPO_NAME = "sd2660_msa"
    }
    stages {
        stage('Docker Login') {
            agent any
            steps {
                withAWS(region: "${REGION}", credentials: 'aws-credential') {
                    script {
                        sh "aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ECR_URI}"
                    }
                }
            }
        }

        stage('Docker Build Frontend') {
            agent any
            steps {
                script {
                    sh "docker build -t ${FRONTEND_APP} src/frontend/"
                    sh "docker tag ${FRONTEND_APP}:latest ${ECR_URI}/${FRONTEND_APP}:${IMAGE_TAG}"
                }
            }
        }

        stage('Scan Frontend Image with Trivy') {
            agent any
            steps {
                script {
                    sh "trivy image --exit-code 1 --severity HIGH,CRITICAL ${FRONTEND_APP}:latest || true"
                }
            }
        }

        stage('Push Frontend Image') {
            agent any
            steps {
                script {
                    sh "docker push ${ECR_URI}/${FRONTEND_APP}:${IMAGE_TAG}"
                }
            }
        }

        stage('Docker Build Backend') {
            agent any
            steps {
                script {
                    sh "docker build -t ${BACKEND_APP} src/backend/"
                    sh "docker tag ${BACKEND_APP}:latest ${ECR_URI}/${BACKEND_APP}:${IMAGE_TAG}"
                }
            }
        }

        stage('Scan Backend Image with Trivy') {
            agent any
            steps {
                script {
                    sh "trivy image --exit-code 1 --severity HIGH,CRITICAL ${BACKEND_APP}:latest || true"
                }
            }
        }

        stage('Push Backend Image') {
            agent any
            steps {
                script {
                    sh "docker push ${ECR_URI}/${BACKEND_APP}:${IMAGE_TAG}"
                }
            }
        }
    }

    post {
        success {
            echo "Docker images pushed successfully!"
        }
        failure {
            echo "There was an error during the Docker build and/or Trivy scan process."
        }
    }
}