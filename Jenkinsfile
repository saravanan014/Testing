pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('Docker')  // Docker Hub credentials
        IMAGE_NAME = "saravana1418/atomui"              // Image name for Trivy scan
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    docker.image(IMAGE_NAME).pull()
                }
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'docker login -u $USERNAME -p $PASSWORD'
                }
            }
        }

        stage('Trivy Scan') {
            steps {
                script {
                    sh "trivy --insecure image $IMAGE_NAME"
                }
            }
        }
    }
}
