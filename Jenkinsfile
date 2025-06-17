pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/kerenyashar/flask-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t kerenyashar/my-flask-app:v1 .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                    sh 'docker push kerenyashar/my-flask-app:v1'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
