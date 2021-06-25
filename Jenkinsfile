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
        sh 'docker images list'
                             
   stage("Docker Login"){
        withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
            sh 'docker login -u liquid07 -p $PASSWORD'
            echo 'DOCKER LOGIN SUSCESS..'
                        }
                                  }
            } 
                         }
    
  
    }
  }
  
}
