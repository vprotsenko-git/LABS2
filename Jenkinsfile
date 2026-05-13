pipeline {
    agent any
    environment {
        PORT = "3001"
        IMAGE_NAME = "nodedev"
        CONTAINER_NAME = "app-dev"
    }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Docker build') {
            steps {
                // Збірка образу для dev (з твоїм новим логотипом)
                sh "docker build -t ${IMAGE_NAME}:v1.0 ."
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Видаляємо ТІЛЬКИ контейнер dev, щоб не чіпати main
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    // Запуск на порту 3001
                    sh "docker run -d --name ${CONTAINER_NAME} -p ${PORT}:3000 ${IMAGE_NAME}:v1.0"
                }
            }
        }
    }
}
