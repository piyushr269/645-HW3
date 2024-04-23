pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'piyushr269/surveyhw3:0.1'
        DOCKER_CREDENTIALS = credentials('docker')
        BUILD_// ID for credentials stored in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm  
            }
        }

        stage('Build and Push docker image') {
            steps {
                script {
                    // Building a Maven project, change if you use Gradle or other build tools
                    sh 'mvn clean package'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("$DOCKER_IMAGE", "./")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry("https://$DOCKER_REGISTRY", DOCKER_CREDENTIALS_ID) {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'kubectl apply -f
                }
            }
        }
    }

    post {
        success {
            echo 'The pipeline has been executed successfully!'
        }
        failure {
            echo 'The pipeline failed.'
        }
    }
}
