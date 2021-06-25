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
     
  }
  
}
