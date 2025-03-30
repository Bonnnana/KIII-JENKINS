pipeline {
    agent any

    environment {
        IMAGE_NAME = 'bojanaandonova/kiii-jenkins'
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build image') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push image') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerImage.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        dockerImage.push("${env.BRANCH_NAME}-latest")
                    }
                }
            }
        }
    }
}

