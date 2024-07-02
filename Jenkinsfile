pipeline {
    agent any
 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('Docker')  // Docker Hub credentials
        IMAGE_NAME = "saravana1418/python-flask-rest-api-project"                         // Image name for Trivy scan
        TRIVY_INSECURE = 'true'                                 // Optional: Disable SSL verification for Trivy
    }
 
    stages {
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
                    sh "trivy image $IMAGE_NAME"
                }
            }
        }
    }
}
