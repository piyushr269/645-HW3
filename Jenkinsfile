 pipeline {
    agent any

   environment {
        DOCKER_IMAGE = 'piyushr269/surveyhw3:0.1'
        DOCKER_CREDENTIALS = credentials('docker')
    DOCKER_TOKEN ='dckr_pat_EJKa9ir1HhdML4MKD97eN4l7Wnw'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Project') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('Build Docker Image') {
            steps {
              withCredentials([string(credentialsId: env.DOCKER_CREDENTIALS, variable: 'DOCKER_TOKEN')]) {
                    sh 'docker login -u piyushr269 -p ${DOCKER_TOKEN}'
                    sh 'docker push piyushr269/surveyhw3:0.1'
                }
                script {
                    docker.build(env.DOCKER_IMAGE)
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', env.DOCKER_CREDENTIALS) {
                        docker.image(env.DOCKER_IMAGE).push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    kubernetesDeploy(
                        configs: 'deployment.yaml',
                        kubeconfigId: env.KUBECONFIG
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
