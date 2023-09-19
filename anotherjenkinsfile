pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the GitHub repo
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                // Build and run tests 
                sh 'npm install'  
                sh 'npm test'     
            }
        }
        stage('Deploy to Render') {
            steps {
                script {
                    def renderCommand = "render deploy"
                    def renderOptions = [
                        "--build-env NODE_ENV=production",
                        "--branch master",  // Git branch to deploy from
                        "--gallery",  
                        "--auto-deploy",  // Automatically deploy when changes are pushed
                        "--wait",  // Wait for the deployment to complete
                    ]
        
                    def fullRenderCommand = "${renderCommand} ${renderOptions.join(' ')}"
        
                    // Execute the Render CLI command
                    sh fullRenderCommand
        }
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


