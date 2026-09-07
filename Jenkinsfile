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
		    API_IMAGE=node-postgres-curd:${BUILD_NUMBER} \
	 	    docker compose \
		      --env-file /etc/node-postgres-curd.env \
		      -p node-js-postgresql-curd-example \
		      up -d	
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
