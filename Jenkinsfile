pipeline {
   agent any
   tools {
       nodejs "NodeJS 20.7.0"
   }
post {
        failure {
            mail to: 'wanguikibiru22@gmail.com',
                 subject: "This pipeline has failed: ${currentBuild.fullDisplayName}",
                 body: "Something is wrong with ${env.BUILD_NUMBER}"
        }
    }
   stages {
       stage('Clone Repo'){
           steps{
               git 'https://github.com/WanguiR/gallery.git'
           }
       }
       stage('install dependancies'){
           steps{
               sh 'npm install'
               sh 'npm install express'
           }
       }
      
       stage('Tests') {
          steps {
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
                        "--auto-deploy",  // Auto deploy when changes are pushed
                        "--wait",  // Wait for the deployment to complete
                    ]
        
                    def fullRenderCommand = "${renderCommand} ${renderOptions.join(' ')}"
        
                    // Execute the Render CLI command
                    sh fullRenderCommand
        }
    }
}

        stage('Notify on slack') {
          steps {
            slackSend color: 'good', message: "id ${env.BUILD_NUMBER} https://hooks.slack.com/services/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", sendAsText: true
          }
       }

   }
}

