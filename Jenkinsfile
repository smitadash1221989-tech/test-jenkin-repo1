pipeline {

    agent any

    tools {
        // This name must exactly match the NodeJS installation
        // configured in Manage Jenkins -> Tools
        nodejs 'NodeJS20'
    }

    environment {
        NODE_ENV = 'QA'
        CI = 'true'
    }

    options {
        timestamps()
        disableConcurrentBuilds()
        buildDiscarder(logRotator(
            numToKeepStr: '10',
            artifactNumToKeepStr: '10'
        ))
    }

    stages {

        stage('Checkout Source') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Display Versions') {
            steps {
                bat 'node --version'
                bat 'npm --version'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing npm packages...'
                bat 'npm ci'
            }
        }

        stage('Install Playwright Browsers') {
            steps {
                echo 'Installing Playwright browsers...'
                bat 'npx playwright install'
            }
        }

        stage('Run Playwright Tests') {
            steps {
                echo 'Executing Playwright tests...'
                bat 'npx playwright test'
            }
        }

        stage('Publish HTML Report') {
            steps {
                publishHTML(target: [
                    allowMissing: true,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'playwright-report',
                    reportFiles: 'index.html',
                    reportName: 'Playwright HTML Report'
                ])
            }
        }

    }

    post {

        success {
            echo '====================================='
            echo ' Playwright Tests Passed'
            echo '====================================='
        }

        failure {
            echo '====================================='
            echo ' Playwright Tests Failed'
            echo '====================================='
        }

        always {

            archiveArtifacts artifacts: '''
                playwright-report/**
                test-results/**
            ''', fingerprint: true

            echo 'Artifacts archived.'
        }

        cleanup {
            cleanWs()
        }
    }
}
