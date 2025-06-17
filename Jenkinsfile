pipeline {
    agent any

    environment {
        IMAGE_NAME = "kerenyashar/my-flask-app:v1"
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/kerenyashar/flask-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
