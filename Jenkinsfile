pipeline {
    agent any

    environment {
        DOCKERHUB_USER   = 'vaishnavi9169'
        BACKEND_IMAGE    = "${DOCKERHUB_USER}/anvit-chat-backend"
        FRONTEND_IMAGE   = "${DOCKERHUB_USER}/anvit-chat-frontend"
    }

    stages {
        stage('Checkout') {
            steps {
                // Jenkins will pull from your Git repo (we'll configure URL in job)
                checkout scm
            }
        }

        stage('Build Docker images') {
            steps {
                bat "docker build -t %BACKEND_IMAGE% ./server"
                bat "docker build -t %FRONTEND_IMAGE% ./client"
            }
        }

        stage('Login & Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-token',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    bat "docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%"
                    bat "docker push %BACKEND_IMAGE%"
                    bat "docker push %FRONTEND_IMAGE%"
                }
            }
        }
    }
}
