pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = 'muhammadshoukat/MLOPS-task-03'
        DOCKER_CREDENTIALS = credentials('d561010a-74bc-4ffb-a4f5-3d8c9bfbf14b/')
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/MuhammadSHOUKATSYED/MLOPS-task-03.git', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_HUB_REPO}:${env.BUILD_ID}")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKER_CREDENTIALS}") {
                        dockerImage.push("${env.BUILD_ID}")
                        dockerImage.push('latest')
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
