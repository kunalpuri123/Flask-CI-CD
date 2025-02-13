pipeline {
    agent any

    environment {
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
                    sh'./docker build -t my-flask-app .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any existing container
                    sh './docker stop ${CONTAINER_NAME} || true'
                    sh './docker rm ${CONTAINER_NAME} || true'

                    // Run the container
                    sh './docker run -d -p 5000:5000 --name ${CONTAINER_NAME} ${DOCKER_IMAGE}'
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    sh 'docker system prune -f'
                }
            }
        }
    }
}
