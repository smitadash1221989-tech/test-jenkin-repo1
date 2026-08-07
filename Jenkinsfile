pipeline {
    agent any

    stages {

        stage('Verify Node') {
            steps {
                bat 'where node'
                bat 'node -v'
                bat 'npm -v'
            }
        }

    }

    post {

        success {
            emailext(
                to: 'smita.dash1221989@gmail.com',
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Hello,

The Jenkins build completed successfully.

Job Name: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}

Regards,
Jenkins
"""
            )
        }

        failure {
            emailext(
                to: 'smita.dash1221989@gmail.com',
                subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Hello,

The Jenkins build has failed.

Job Name: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}

Please check the Jenkins console output.

Regards,
Jenkins
"""
            )
        }

    }
}
