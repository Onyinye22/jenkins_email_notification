pipeline {
    agent any

    environment {
        // Define email-related environment variables
        RECIPIENTS = 'estheronyinye011@gmail.com, goodnessm508@gmail.com, ijeonyinye22@gmail.com, danielofurutech@gmail.com, guddytechs@gmail.com'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                git url: 'https://github.com/Goodyoma/jenkins-email-notification.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // Simulate a build step
                sh 'echo "Building project..."'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                // Simulate a test step
                sh 'echo "Running tests..."'
            }
        }
    }

    post {
        always {
            // Send an email notification after every build
            script {
                emailext(
                    subject: "Jenkins Job: ${currentBuild.fullDisplayName}",
                    body: """<p>Build ${currentBuild.fullDisplayName} has completed.</p>
                             <p>Result: ${currentBuild.currentResult}</p>
                             <p>Check console output at <a href="${env.BUILD_URL}">${env.BUILD_URL}</a> to view the results.</p>""",
                    recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'CulpritsRecipientProvider']],
                    to: "${env.RECIPIENTS}",
                    mimeType: 'text/html'
                )
            }
        }
        success {
            script {
                emailext(
                    subject: "SUCCESS: Jenkins Job ${currentBuild.fullDisplayName}",
                    body: """<p>Build ${currentBuild.fullDisplayName} was successful.</p>
                             <p>Result: ${currentBuild.currentResult}</p>
                             <p>Check console output at <a href="${env.BUILD_URL}">${env.BUILD_URL}</a> to view the results.</p>""",
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                    to: "${env.RECIPIENTS}",
                    mimeType: 'text/html'
                )
            }
        }
        failure {
            script {
                emailext(
                    subject: "FAILURE: Jenkins Job ${currentBuild.fullDisplayName}",
                    body: """<p>Build ${currentBuild.fullDisplayName} failed.</p>
                             <p>Result: ${currentBuild.currentResult}</p>
                             <p>Check console output at <a href="${env.BUILD_URL}">${env.BUILD_URL}</a> to view the results.</p>""",
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                    to: "${env.RECIPIENTS}",
                    mimeType: 'text/html'
                )
            }
        }
    }
}
