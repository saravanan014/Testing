pipeline {
    agent any
    environment {
        TRIVY_INSECURE = 'true'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                    sh 'docker login -u $USERNAME -p $PASSWORD'
                }
            }
        }
        stage('Trivy Scan') {
            steps {
                sh 'trivy image saravana1418/python-flask-rest-api-project'
            }
        }
    }
}
