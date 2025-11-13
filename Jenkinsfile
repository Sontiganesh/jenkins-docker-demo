pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "sontiganesh/jenkins-docker-demo"
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

        stage('Push to Docker Hub') {
            steps {
                echo "Pushing image to Docker Hub..."
                withCredentials([usernamePassword(credentialsId: '326dfe2c-5f46-4a12-b105-b201995f054e', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push $DOCKER_IMAGE:latest'
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                echo "Deploying container on EC2..."
                // We'll add actual EC2 deployment next
            }
        }

        stage('Cleanup') {
            steps {
                echo "Cleaning up local image..."
                sh 'docker rmi -f $DOCKER_IMAGE:latest || true'
            }
        }
    }
}
