pipeline {
    agent any

    tools {
        nodejs 'node16'
    }

    //environment {
    //    SCANNER_HOME = tool 'sonar-scanner'
   // }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/jaiswaladi246/fullstack-bank.git'
            }
        }

        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '--scan ./app/backend --disableYarnAudit --disableNodeAudit', odcInstallation: 'DC'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }

        stage('Trivy File System Scan') {
            steps {
                sh "trivy fs ."
            }
        }

        // Uncomment and update for SonarQube analysis if needed
        /*
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh "$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Bank -Dsonar.projectKey=Bank"
                }
            }
        }
        */

        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }

        stage('Backend Setup') {
            steps {
                dir('app/backend') {
                    sh "npm install"
                }
            }
        }

        stage('Frontend Setup') {
            steps {
                dir('app/frontend') {
                    sh "npm install"
                }
            }
        }

        stage('Deploy to Container') {
            steps {
                sh "npm run compose:up -d"
            }
        }
    }
}
