pipeline {
   agent any
 
   environment {
       DOCKERHUB_CREDENTIALS = credentials('Docker')  // Docker Hub credentials
       IMAGE_NAME = "saravana1418/python-flask-rest-api-project"                         // Image name for Trivy scan
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
                 sh "sudo trivy --insecure image $IMAGE_NAME"
               }
           }   
       }
   }
}
