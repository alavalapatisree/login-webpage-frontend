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
                    bat "\"C:\\Program Files\\Java\\jdk-17\\bin\\jar\" -cvf front-end.war -C build ."


                }
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Copy the WAR file to Tomcat webapps directory
                    def tomcatWebapps = 'C:/path/to/tomcat/webapps'
                    bat "copy front-end.war ${tomcatWebapps}"
                }
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
