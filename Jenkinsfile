pipeline {
    agent any
    tools{
        maven 'Maven9.9.9'
    }

    stages {
        stage('Clone the repository ') {
            steps {
                
             git branch: 'build-and-push-to-jfrog-jenkinsfile', credentialsId: 'd427e0c7-b3b4-434f-94fc-caa5ff96258d', url: 'https://github.com/Manideepthaduriias/java-application.git'
                
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
