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
                    bat "C:/Program Files/Java/jdk-17/bin/jar -cvf ${WAR_FILE} -C path/to/your/app ."

                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    def tomcatUrl = 'http://localhost:8080'  // Update the URL if your Tomcat is running on a different port
                    def tomcatManagerUser = 'admin'  // Update with your Tomcat manager username
                    def tomcatManagerPassword = 'admin'  // Update with your Tomcat manager password
                    def warFileName = 'front-end.war'  // Update with the actual WAR file name

                    // Deploy the WAR file to Tomcat using the manager API
                    sh "curl -v --user ${tomcatManagerUser}:${tomcatManagerPassword} --upload-file build/${warFileName} ${tomcatUrl}/manager/text/deploy?path=/front-end"
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
