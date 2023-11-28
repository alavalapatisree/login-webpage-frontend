pipeline {
    agent any

    environment {
        npm = bat(script: 'where npm', returnStatus: true).trim()
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    bat "${npm} install"
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    bat "${npm} run build"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Add your deployment steps here
                }
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed!'
        }
    }
}
