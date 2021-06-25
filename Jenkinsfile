pipeline {

  agent any

  stages {

    stage('Git Clone') {
      steps {
        
          git credentialsId: 'GIT_HUB_CREDENTIALS', url: 'https://github.com/patiwat13/nginx-say.git'
            }
                       }
    
     stage('Docker build'){
       step {

          sh 'docker version'
          sh 'docker build -t nginx-docker-demo .'
          sh 'docker image list'
          sh 'docker tag nginx-docker-demo liquid07/nginx-docker-demo:nginx-docker-demo'
            }
       }
    
    
    }
  
}
      
