pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "aryanakhare/e-com:latest"
    }
    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Clone the Git repository
                    try {
                        git 'https://github.com/SRCEM-AIM-Class-A/A21-AryanAkhare-SL3-3.git'
                    } catch (Exception e) {
                        error "Git Clone failed: ${e.message}"
                    }
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    try {
                        // Build the Docker image
                        docker.build(DOCKER_IMAGE)
                    } catch (Exception e) {
                        error "Docker build failed: ${e.message}"
                    }
                }
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: '6566fbd1-d493-4162-bdca-6a3b8778c112', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    script {
                        try {
                            // Log into Docker Hub using credentials
                            sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                        } catch (Exception e) {
                            error "Docker login failed: ${e.message}"
                        }
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    try {
                        // Push the Docker image to Docker Hub
                        docker.push(DOCKER_IMAGE)
                    } catch (Exception e) {
                        error "Docker push failed: ${e.message}"
                    }
                }
            }
        }
    }
    post {
        always {
            // Clean up the workspace after the pipeline completes
            cleanWs()
        }
    }
}
