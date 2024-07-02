pipeline {
    agent any
 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')  // Docker Hub credentials
        IMAGE_NAME = "saravana1418/python-flask-rest-api-project"                         // Image name for Trivy scan
    }
 
    stages {
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'docker login -u $USERNAME -p $PASSWORD'
                }
            }
        }
 
        stage('Trivy Scan') {
            steps {
                script {
                  sh "trivy image $IMAGE_NAME"
                }
            }   
        }
    }
}
