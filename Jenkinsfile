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
                sh 'mvn clean package' // Usually, you want to run package to compile and package your application
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', credentials(DOCKER_CREDENTIALS_ID)) {
                        def customImage = docker.build(DOCKER_IMAGE)
                        customImage.push() // Combine build and push in one stage for simplicity and to use only one login session
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    kubernetesDeploy(
                        configs: 'deployment.yaml', // Ensure you have the correct path to your Kubernetes deployment file
                        kubeconfigId: 'kubeconfig-id' // Specify the ID of your Kubernetes configuration stored in Jenkins credentials
                    )
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
