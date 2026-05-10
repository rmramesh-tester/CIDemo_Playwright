pipeline {

    agent any

    tools {
        nodejs 'NodeJS'
    }

    triggers {
        cron('10 22 * * *')
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/yourusername/playwright-framework.git'
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

        stage('Generate Playwright HTML Report') {
            steps {
                bat 'npx playwright show-report'
            }
        }
    }

    post {

        always {

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