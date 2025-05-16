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
                sh 'npm install'
            }
        }
        stage('Run tests') {
            steps {
                sh 'npm test'
            }
        }
        stage('Generate coverage report') {
            steps {
                sh 'npm run coverage'
            }
        }
        stage('Run audit scan') {
            steps {
                sh 'npm audit'
            }
        }
    }
}
