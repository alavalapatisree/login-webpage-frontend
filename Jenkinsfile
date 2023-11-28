pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from Git
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                // Install Node.js and npm
                bat 'npm install'

                // Build and test your Node.js application
                bat 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // Your deployment steps (if any)
            }
        }
    }

    post {
        always {
            // Cleanup steps, if any
        }
    }
}
