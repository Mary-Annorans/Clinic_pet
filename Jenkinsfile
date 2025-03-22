pipeline {
    agent any

    environment {
        IMAGE = 'spring-petclinic'
        DOCKERHUB_USER = 'maryann123456789'  // Replace with your actual DockerHub username
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker stop petclinic || true
                    docker rm petclinic || true
                    docker run -d --name petclinic -p 8081:8080 $IMAGE
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build and Deployment Successful!'
        }
        failure {
            echo '❌ Build Failed!'
        }
    }
}
