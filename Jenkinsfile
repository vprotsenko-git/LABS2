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
                // Збірка образу для main
                sh "docker build -t ${IMAGE_NAME}:v1.0 ."
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Видаляємо ТІЛЬКИ контейнер main, щоб не чіпати dev
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    // Запуск на порту 3000
                    sh "docker run -d --name ${CONTAINER_NAME} -p ${PORT}:3000 ${IMAGE_NAME}:v1.0"
                }
            }
        }
    }
}
