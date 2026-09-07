pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t node-postgres-crud:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker compose \
                      --env-file /etc/node-postgres-crud.env \
                      -p node-js-postgresql-crud-example \
                      up -d --build
                '''
            }
        }

        stage('Smoke Test') {
            steps {
                sh 'curl --fail http://localhost:8080'
            }
        }
    }
}
