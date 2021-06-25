pipeline {

  agent any

  stages {

    stage('Git Clone') {
      steps {
         script {
          git credentialsId: 'GIT_HUB_CREDENTIALS', url: 'https://github.com/patiwat13/nginx-say.git'
          sh 'pwd'
            }
      }
                       }
    
    stage("Docker build"){
        steps {
                           script {
        sh 'docker version'
        sh 'docker build -t nginx-docker-jenkins .'
        sh 'docker image list'
        sh 'docker tag nginx-docker-jenkins liquid07/nginx-docker-demo:jenkins-nginx'
                           }
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
    
                            echo 'SSH Success'
                 
                  stage('Using Command') {
                   sshCommand remote: remote, command: 'docker version' 
                  }
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
