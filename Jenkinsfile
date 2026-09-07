pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t node-postgres-crud:${BUILD_NUMBER} .'
            }
        }
    }
}
