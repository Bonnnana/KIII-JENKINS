pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub'           
        IMAGE_NAME = 'bojanaandonova/kiii-jenkins'    
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        dockerImage.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        dockerImage.push("${env.BRANCH_NAME}-latest")
                    }
                }
            }
        }
    }
}

