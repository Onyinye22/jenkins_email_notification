pipeline {
    agent any

    environment {
        // Set email addresses for notification
        RECIPIENTS = 'estheronyinye011@gmail.com, danielofurutech@gmail.com, goodnessm508@gmail.com.com, guddytechs@gmail.com'
        SENDER = 'estheronyinye011@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Your build steps go here
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Your test steps go here
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Your deploy steps go here
            }
        }
    }

    post {
        success {
            script {
                emailext(
                    subject: "Jenkins Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """<p>Good news!</p>
                             <p>Build <b>${env.JOB_NAME} #${env.BUILD_NUMBER}</b> was successful.</p>
                             <p>Check the details <a href="${env.BUILD_URL}">here</a>.</p>""",
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                    to: "${RECIPIENTS}",
                    from: "${SENDER}"
                )
            }
        }
        failure {
            script {
                emailext(
                    subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """<p>Unfortunately,</p>
                             <p>Build <b>${env.JOB_NAME} #${env.BUILD_NUMBER}</b> failed.</p>
                             <p>Check the details <a href="${env.BUILD_URL}">here</a>.</p>""",
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                    to: "${RECIPIENTS}",
                    from: "${SENDER}"
                )
            }
        }
        always {
            script {
                emailext(
                    subject: "Jenkins Build Completed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """<p>Build <b>${env.JOB_NAME} #${env.BUILD_NUMBER}</b> has completed.</p>
                             <p>Result: ${currentBuild.currentResult}</p>
                             <p>Check the details <a href="${env.BUILD_URL}">here</a>.</p>""",
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                    to: "${RECIPIENTS}",
                    from: "${SENDER}"
                )
            }
        }
    }
}
