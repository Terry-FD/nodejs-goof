pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run tests') {
            steps {
                bat 'npm test'
            }
        }
        stage('Generate coverage report') {
            steps {
                bat 'npm run coverage'
            }
        }
        stage('Run audit scan') {
            steps {
                bat 'npm audit'
            }
        }
    }
}
