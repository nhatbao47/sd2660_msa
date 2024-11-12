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
        stage('Docker Build Frontend') {
            agent any
            steps {
                withAWS(region:'us-east-1',credentials:'aws-credential') {
                    sh "aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ECR_URI}"
                    sh "docker build -t ${FRONTEND_APP} src/frontend/"
                    sh "docker tag ${FRONTEND_APP}:latest ${ECR_URI}/${FRONTEND_APP}:${IMAGE_TAG}"
                    sh "docker push ${ECR_URI}/${FRONTEND_APP}:${IMAGE_TAG}"
                }
            }
        }
        stage('Docker Build Backend') {
            agent any
            steps {
                withAWS(region:'us-east-1',credentials:'aws-credential') {
                    sh "aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ECR_URI}"
                    sh "docker build -t ${BACKEND_APP} src/backend/"
                    sh "docker tag ${BACKEND_APP}:latest ${ECR_URI}/${BACKEND_APP}:${IMAGE_TAG}"
                    sh "docker push ${ECR_URI}/${BACKEND_APP}:${IMAGE_TAG}"
                }
            }
        }
    }
}