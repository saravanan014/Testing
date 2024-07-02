pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('Docker')  // Docker Hub credentials ID
        IMAGE_NAME = "saravana1418/atomui"              // Image name for Trivy scan
    }

    stages {
        stage('Docker Login') {
            steps {
                script {
                    // Login to Docker Hub
                    withCredentials([usernamePassword(credentialsId: 'Docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                    }
                }
            }
        }

        stage('Pull Docker Image') {
            steps {
                script {
                    // Pull the Docker image if not already present
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        def customImage = docker.image("${IMAGE_NAME}")
                        if (!customImage.exists()) {
                            customImage.pull()
                        }
                    }
                }
            }
        }

        stage('Trivy Scan') {
            steps {
                script {
                    // Run Trivy scan on the Docker image
                    sh "trivy --insecure image ${IMAGE_NAME}"
                }
            }
        }
    }
}
