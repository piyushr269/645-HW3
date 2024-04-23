pipeline {
    agent any

    tools {
        // Make sure Maven is configured in Jenkins Global Tool Configuration
        maven 'Maven 3.6.3'
        // Make sure Java is configured in Jenkins Global Tool Configuration
        jdk 'OpenJDK 11'
    }

    environment {
        // Define the variable for the JAR filename
        JAR_FILE = 'target/SpringBoot-0.0.1-SNAPSHOT.jar'
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out the source code from version control
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Run Maven build
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                // Archive the built JAR file
                archiveArtifacts artifacts: "${env.JAR_FILE}", onlyIfSuccessful: true
            }
        }

        stage('Deploy') {
            when {
                // This could be changed to a condition like branch == 'main'
                expression { env.BRANCH_NAME == 'main' }
            }
            steps {
                // Add steps to deploy the JAR file to your server/environment
                echo 'Deploying application...'
                // Example: sh 'scp ${env.JAR_FILE} user@server:/path/to/deploy'
            }
        }
    }

    post {
        success {
            echo 'Build and archive steps completed successfully.'
        }
        failure {
            echo 'The build failed.'
        }
    }
}
