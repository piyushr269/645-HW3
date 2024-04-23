pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'piyushr269/surveyhw3:0.1'
        DOCKER_CREDENTIALS_ID = 'docker' // Use a descriptive ID for credentials
    }

     stage('Build') {
            steps {
                echo 'Running build steps'
                // Simulate a build command, e.g., compiling a Java project:
                // sh 'mvn clean package'
                sh 'echo "Building the project..."'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
                // Simulate running tests, e.g., running unit tests with Maven:
                // sh 'mvn test'
                sh 'echo "Running tests..."'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'
                // Simulate a deployment step
                sh 'echo "Deploying to staging server..."'
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
