pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('akashrad-dockerhub')
        DOCKER_DEV_IMAGE = 'akashrad/dev:latest'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_DEV_IMAGE)
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('', DOCKER_HUB_CREDENTIALS) {
                        docker.image(DOCKER_DEV_IMAGE).push()
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}

