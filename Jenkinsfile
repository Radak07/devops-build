pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('akashrad-dockerhub')
        DOCKER_PROD_IMAGE = 'akashrad/prod:latest'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_PROD_IMAGE)
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('', DOCKER_HUB_CREDENTIALS) {
                        docker.image(DOCKER_PROD_IMAGE).push()
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
