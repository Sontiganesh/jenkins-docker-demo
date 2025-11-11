pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ganeshdemo/jenkins-docker-demo"
    }

    stages {
        stage('Clone') {
            steps {
                echo "Cloning repository..."
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }

        stage('Run Container') {
            steps {
                echo "Running container..."
                sh 'docker run --rm $DOCKER_IMAGE:latest'
            }
        }

        stage('Cleanup') {
            steps {
                echo "Removing image..."
                sh 'docker rmi -f $DOCKER_IMAGE:latest || true'
            }
        }
    }
}
