pipeline {
    agent any

 tools {
        nodejs 'nodejs'
    }

    environment {
        TOMCAT_URL = 'http://localhost:8081'  // Replace with your Tomcat URL
        TOMCAT_USER = 'admin'
        TOMCAT_PASS = 'admin'
        APP_NAME = 'front-end'           // Replace with your Node.js application name
        WAR_FILE = "${APP_NAME}.war"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Your build steps (e.g., npm install) go here
                    // Example: sh 'npm install'
                    // Install Node.js and npm
                    bat 'npm install'

                    // Build and test your Node.js application
                    bat 'npm run build'
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    // Create a WAR file for deployment
                    sh 'npm run build'
                    sh 'jar -cvf ${WAR_FILE} -C path/to/your/app .'
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Deploy the WAR file to Tomcat
                    sh "curl -v --upload-file ${WAR_FILE} ${TOMCAT_URL}/manager/text/deploy?path=/${APP_NAME}"
                }
            }
        }
    }

    post {
        always {
            // Clean up after the build
            cleanWs()
        }
    }
}
