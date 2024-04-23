pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'piyushr269/surveyhw3:0.1'
        DOCKER_CREDENTIALS_ID = 'docker' // Use a descriptive ID for credentials
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Project') {
            steps {
                sh 'mvn clean ' // Usually, you want to run package to compile and package your application
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
               
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
