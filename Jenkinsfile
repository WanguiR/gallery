pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your code from the GitHub repository
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                // Build and run tests for your application
                sh 'npm install'  // Replace with your build commands
                sh 'npm test'     // Replace with your test commands
            }
        }

        stage('Deploy to Render') {
            steps {
                // Use Render's CLI (or API) to deploy your application
                sh 'render deploy -- --build-env NODE_ENV=production'
            }
        }
    }

    post {
        success {
            echo 'Deployment to Render successful!'
        }
        failure {
            echo 'Deployment to Render failed!'
        }
    }
}


