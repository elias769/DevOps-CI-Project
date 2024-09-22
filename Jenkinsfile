pipeline {
    agent any

    tools {
        nodejs 'node16' // Ensure Node.js is installed and configured as 'node16'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'npm run test'
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

        stage('Deploy using Docker Compose') {
            steps {
                sh 'npm run compose:up -d'
            }
        }

        // Uncomment this stage if you want to stop the containers afterward
        /*
        stage('Stop Docker Containers') {
            steps {
                sh 'npm run compose:down'
            }
        }
        */
    }
}
