pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "aryanakhare/e-com:latest"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/SRCEM-AIM-Class-A/A21-AryanAkhare-SL3-3.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: '6566fbd1-d493-4162-bdca-6a3b8778c112', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.push(DOCKER_IMAGE)
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
