pipeline {
    agent any
    tools{
        maven "maven3.9.9"
    }
    stages {
      stage('Clone the repository'){
        steps{
          git branch: 'pushing-docker-image-to-dockerhub-jenkinsfile', credentialsId: '84f26f86-f84b-4a19-946f-b266aa383022', url: 'https://github.com/Manideepthaduriias/java-application.git'ion.git'
          
        } 
      }
      
  stage('Build the code') {
            steps {
                sh 'mvn clean install'
            }
        }    
      
 stage('Build Docker Image') {
            steps {
                sh '''
               docker build . --tag web-application:$BUILD_NUMBER
               docker tag web-application:$BUILD_NUMBER manideepk8s/web-application:$BUILD_NUMBER
                
                '''
                
            }
        }
        stage('Push Docker Image') {
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub-username-password', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                 sh '''
                 docker login -u $DOCKERHUB_USERNAME   -p $DOCKERHUB_PASSWORD
                  docker push manideepk8s/web-application:$BUILD_NUMBER
                    
                   ''' 

            }
            
        }
      
    }
}
