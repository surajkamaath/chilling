pipeline {
    agent any

    environment {
        IMAGE_NAME = "surajkamathh/myapp"
        IMAGE_TAG = "v1"
    }

    stages {

        stage('Docker Check') {
            steps {
                bat "docker --version"
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_TOKEN'
                )]) {
                    bat '''
                    docker logout
                    docker login -u %DOCKER_USER% -p %DOCKER_TOKEN%
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME%:%IMAGE_TAG% ."
            }
        }

        stage('Push Docker Image') {
            steps {
                bat "docker push %IMAGE_NAME%:%IMAGE_TAG%"
            }
        }
    }
}