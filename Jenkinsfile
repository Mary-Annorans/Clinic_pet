pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Mary-Annorans/Clinic_pet.git'
            }
        }

        stage('Build with Maven') {
            steps {
                script {
                    docker.image('maven:3.9.9').inside {
                        sh 'mvn clean package'
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t clinic_pet_image .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8080:8080 --name clinic_pet_container clinic_pet_image'
            }
        }
    }

    post {
        failure {
            echo '❌ Build Failed!'
        }
        success {
            echo '✅ Build Succeeded!'
        }
    }
}

