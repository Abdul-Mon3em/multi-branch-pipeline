pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                // Install dependencies
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                // Run tests
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                // Deploy to development environment
                sh './jenkins/scripts/deliver-for-development.sh'
                // Manual approval
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                // Clean up
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                // Deploy to production environment
                sh './jenkins/scripts/deploy-for-production.sh'
                // Manual approval
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                // Clean up
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}

