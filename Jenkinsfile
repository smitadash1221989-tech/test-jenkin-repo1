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
}
