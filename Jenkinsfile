pipeline {
    agent any  
    
    environment {
        RECIPIENTS = 'guddytechs@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Add your build steps here
                    echo 'Building...'
                    // Example: sh 'make build'
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Add your test steps here
                    echo 'Testing...'
                    // Example: sh 'make test'
                }
            }
        }
    }

    post {
        always {
            script {
                emailext(
                    subject: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """
                        <p>Build Status: ${currentBuild.currentResult}</p>
                        <p>Project: ${env.JOB_NAME}</p>
                        <p>Build Number: ${env.BUILD_NUMBER}</p>
                        <p>Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                    """,
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                    to: "${env.RECIPIENTS}",
                    mimeType: 'text/html'
                )
            }
        }
    }
}
