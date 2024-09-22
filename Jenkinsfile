pipeline {
    agent any

    tools {
        nodejs 'node16' // Make sure Node.js 16 is installed on Jenkins
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Start Containers') {
            steps {
                sh 'npm run compose:up'
            }
        }

        stage('Run Integration Tests') {
            steps {
                sh 'npm run test:integration'
            }
        }

        stage('Run E2E Tests') {
            steps {
                sh 'npm run test:e2e'
            }
        }

        // Uncomment if you want to bring the containers down after tests
        /*
        stage('Stop Containers') {
            steps {
                sh 'npm run compose:down'
            }
        }
        */
    }

    post {
        always {
            echo 'Cleaning up resources...'
            // Ensure containers are stopped regardless of build status
            sh 'npm run compose:down || true'
        }
    }
}
