pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_FILE = 'docker-compose.yml'
        // If you have any specific Docker Hub credentials
        DOCKER_CREDENTIALS = 'dockerhub-credentials' 
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull the latest code from the GitHub repository
                git branch: 'master', url: 'https://github.com/yourusername/yourrepository.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    // Build Docker images using docker-compose
                    sh 'docker-compose -f $DOCKER_COMPOSE_FILE build'
                }
            }
        }

        stage('Deploy Containers') {
            steps {
                script {
                    // Start containers using docker-compose up
                    sh 'docker-compose -f $DOCKER_COMPOSE_FILE up -d'
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    // Optionally clean up resources if needed
                    sh 'docker-compose down'
                }
            }
        }
    }

    post {
        always {
            // Archive build logs or any other artifacts if needed
            echo 'Pipeline execution completed!'
        }
    }
}
