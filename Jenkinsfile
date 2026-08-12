pipeline{
    agent any
    stages{
        stage('checkout')
        {
            steps{
                 checkout scm
            }
        }
        stage('Install Dependencies')
        {
            steps{
                bat 'npm ci'
            }
        }
        stage('Install Playwright')
        {
            steps{
                bat 'npx playwright install'
            }
        }
        stage('Run Tests')
        {
            steps{
                bat 'npx playwright test'
            }
        }

    }
    post{
        always{
            archiveArtifacts(
                artifacts:'playwright-report/**,test-result/**',
                allowEmptyArchive:true
            )
        }
        success{
            echo "playwright run success"
        }
        failure{
            echo "playwright test failed"
        }
    }
}