pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'surveyhw3:0.1'
        DOCKER_REGISTRY = 'piyushr269/surveyhw3:0.1'
        DOCKER_CREDENTIALS_ID = 'docker'  // ID for credentials stored in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/piyushr269/645-HW3.git'  // Your repository URL
            }
        }

        stage('Build Application') {
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
                    // Deployment step, modify according to your deployment logic
                    sh 'echo Deploying application...'
                    // For example, if you deploy via SSH, you might use an ssh command to run docker commands on a remote server
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
