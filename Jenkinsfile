pipeline {
    environment {
        DOCKERHUB_CREDENTIALS = credentials('davingreg-dockerhub')
    }
    agent any
    stages {
        stage('Cloning Git Repository') {
            steps {
                git 'https://github.com/GregoriusDavin/welcome-to-docker.git'
            }
        }

        stage('Building Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Deploying Docker Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Cleaning up') {
            steps {
                sh "docker rmi ${registry}:${BUILD_NUMBER}"
            }
        }
    }

    post {
        success {
            echo 'Pipeline successfully completed. Image deployed and cleaned up.'
        }

        failure {
            echo 'Pipeline failed. Please check the logs for details.'
        }
    }
}
