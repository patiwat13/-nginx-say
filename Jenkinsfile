pipeline {

  agent any

  stages {

    stage('Git Clone') {
      steps {
        
          git credentialsId: 'GIT_HUB_CREDENTIALS', url: 'https://github.com/patiwat13/nginx-say.git'
            }
                       }
     
  //state 'echo ssh mv'
    stage('SSH into the server') {
        steps {
               script {
                            def remote = [:]
                            remote.name = 'K8S master'
                            remote.host = '192.168.1.100'
                            remote.user = 'root'
                            remote.password = 'zjkoC]6p'
                            remote.allowAnyHosts = true
    
                            sh 'docker version'
               }
        }
    }
     stage('Docker build') {
       steps {
              script {
          //sh 'sudo apt install docker.io'
          sh 'docker version'
          //sh 'docker build -t nginx-docker-demo .'
          //sh 'docker image list'
          //sh 'docker tag nginx-docker-demo liquid07/nginx-docker-demo:nginx-docker-demo'
                      }
              }
                          }
            
            }
      

}
