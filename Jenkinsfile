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
        subject: 'Jenkins Success Test',
        body: 'This is a test email from the Jenkins pipeline.'
    )
}
      

    }
}
