pipeline {
    agent any
    tools{
        maven 'Maven3.8.7'
    }

    stages {
        stage('Clone the repository ') {
            steps {
                
             git branch: 'build-and-push-to-jfrog-jenkinsfile', credentialsId: 'gitcredentials', url: 'https://github.com/Manideepthaduriias/java-application.git'
                
            }
        }
       
       stage("Build the code") {
           
           steps{
               sh 'mvn clean install'
           }
       }
      stage('Push the artifacts into Jfrog artifactory') {
            steps {
              rtUpload (
                serverId: 'jfrog-dev-server',
                spec: '''{
                      "files": [
                        {
                          "pattern": "*.war",
                           "target": "web-application/"
                        }
                    ]
                }'''
              )
          }
        }
     
        
        
        
    }
}
