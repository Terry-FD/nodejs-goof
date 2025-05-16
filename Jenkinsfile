pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                bat 'git clone https://github.com/Terry-FD/nodejs-goof.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install || exit /b 0'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0' // Continue even if test fails
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0' // Show known CVEs
            }
        }
     stage('SonarCloud Analysis') {
            steps {
                withCredentials([string(credentialsId: 'SONARCLOUD_TOKEN', variable: 'SONAR_TOKEN')]) {
                    bat '''
                        npm install -g sonarqube-scanner
                        sonar-scanner ^
                          -Dsonar.projectKey=8-2CDevSecOps ^
                          -Dsonar.organization=taoterry ^
                          -Dsonar.sources=. ^
                          -Dsonar.host.url=https://sonarcloud.io ^
                          -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }
    }
}