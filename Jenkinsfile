pipeline {
    agent any


    environment {
        // Define the variable for the JAR filename
         DOCKERHUB_PASS = credentials("docker")
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
                sh 'rm -rf var'
                sh 'jar -cvf SpringBoot-0.0.1-SNAPSHOT.jar -C src/main/webapp/ .'
                def BUILD_TIMESTAMP = sh(script: 'date +%Y%m%d%H%M%S', returnStdout: true).trim()
                sh "docker login -u piyushr269 -p ${DOCKERHUB_PASS}"
                sh "docker build -t piyushr269/surveyhw3:${0.1} ."
                sh "docker push piyushr269/surveyhw3:${0.1}"
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
