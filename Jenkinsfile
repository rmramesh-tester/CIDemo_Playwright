pipeline {

    agent any

    tools {
        nodejs 'NodeJS'
    }

    triggers {
        cron('36 22 * * *')
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/rmramesh-tester/CIDemo_Playwright.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Install Playwright Browsers') {
            steps {
                bat 'npx playwright install'
            }
        }

        stage('Execute Playwright Tests') {
            steps {
                bat 'npx playwright test'
            }
        }
    }

    post {

        always {

            bat 'npx playwright show-report'

            emailext(
                subject: "Playwright Build Status: ${currentBuild.currentResult}",

                body: """
                Build Status: ${currentBuild.currentResult}

                Job Name: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}

                Build URL:
                ${env.BUILD_URL}
                """,

                to: 'rmramesh.testing@gmail.com'
            )
        }
    }
}