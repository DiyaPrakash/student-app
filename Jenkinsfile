pipeline {
    agent any

    environment {
        DOCKERHUB_USERNAME = "diyaprakash"
        IMAGE_FRONTEND = "${DOCKERHUB_USERNAME}/bcs28-frontend"
        IMAGE_BACKEND = "${DOCKERHUB_USERNAME}/bcs28-backend"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/YOUR_REPO.git'
            }
        }

        stage('Build Images') {
            steps {
                sh 'docker build -t $IMAGE_FRONTEND:latest ./frontend'
                sh 'docker build -t $IMAGE_BACKEND:latest ./backend'
            }
        }

        stage('DockerHub Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Images') {
            steps {
                sh 'docker push $IMAGE_FRONTEND:latest'
                sh 'docker push $IMAGE_BACKEND:latest'
            }
        }

       
    }
}