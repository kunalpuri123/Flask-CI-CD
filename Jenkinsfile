pipeline {
    agent any

    environment {
        DOCKER_PATH = "/usr/local/bin/docker"
        DOCKER_IMAGE = "flask-app"
        CONTAINER_NAME = "flask-container"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/kunalpuri123/Flask-CI-CD.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh '${DOCKER_PATH} build -t ${DOCKER_IMAGE} .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any existing container
                    sh '${DOCKER_PATH} stop "$CONTAINER_NAME" || true'
                    sh '${DOCKER_PATH} rm "$CONTAINER_NAME" || true'

                    // Run the container
                    sh '${DOCKER_PATH} run -d -p 5001:5000 --name "$CONTAINER_NAME" "$DOCKER_IMAGE"'
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    sh '${DOCKER_PATH} system prune -f'
                }
            }
        }
    }
}
