pipeline {
    agent any
 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker')  // Docker Hub credentials
        IMAGE_NAME = "saravana1418/nginx"                         // Image name for Trivy scan
    }
 
    stages {
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
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
