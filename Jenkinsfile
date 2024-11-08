pipeline {
    agent any
    tools{
        maven "maven3.9.9"
    }

    stages {
        stage('Clone the repository') {
            steps {
               git branch: 'build-and-deploy-to-tomcat-jenkinsfile', credentialsId: '67241ba2-0e77-4f62-9daa-d1fde0bfc788', url: 'https://github.com/Manideepthaduriias/java-application.git'
            }
        }
        
        stage('Build the code') {
            steps {
            sh 'mvn clean install'
                
            }
        }
        
        stage('Deploy to tomcat') {
            steps {
            deploy adapters: [tomcat7(credentialsId: 'Tomcat-7-cred', path: '', url: 'http://100.25.166.179:8080')], contextPath: null, war: '**/*.war'
                
            }
        }
    }
}
