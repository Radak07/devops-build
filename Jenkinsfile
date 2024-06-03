
pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('akashrad-dockerhub')
        DOCKER_REPO = 'akashrad/prod'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Radak07/devops-build.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${env.DOCKER_REPO}:${env.BUILD_ID}")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'akashrad-dockerhub') {
                        dockerImage.push("${env.BUILD_ID}")
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}
