pipeline {
    agent any
    environment {
        PORT = "3000"
        IMAGE_NAME = "nodemain"
        CONTAINER_NAME = "app-main"
    }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Docker build') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:v1.0 ."
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    sh "docker run -d --name ${CONTAINER_NAME} -p ${PORT}:3000 ${IMAGE_NAME}:v1.0"
                }
            }
        }
    }
}
