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
        sh 'docker build -t nginx-docker-demo .'
        sh 'docker image list'
        sh 'docker tag nginx-docker-demo liquid07/nginx-docker-demo:nginx-docker-demo'
        sh 'docker images list'
                             
    stage("Docker Login"){
        withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
            sh 'docker login -u liquid07 -p $PASSWORD'
            echo 'DOCKER LOGIN SUCESS..'
                        }
                                  }
                             
      stage("Push Image to Docker Hub"){
        sh 'docker push  liquid07/nginx-docker-demo:nginx-docker-demo'
        echo 'Push Sucess!!'
    }
                             
         stage("SSH Into Virtual machine Server") {
        def remote = [:]
        remote.name = 'K8S master'
        remote.host = '172.20.5.66'
        remote.user = 'patiwat'
        remote.password = 'patiwat#123'
        remote.allowAnyHosts = true

        stage('Put nginx-deployment.yaml onto k8s master') {
            sshPut remote: remote, from: 'nginx-deployment.yaml', into: '.'

        }
        stage("Login to Microk8s"){
  kubeconfig(caCertificate: 'LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUREekNDQWZlZ0F3SUJBZ0lVWWorNHJDWXFWUFpvWU1uRG9aYzhSQmRycE9jd0RRWUpLb1pJaHZjTkFRRUwKQlFBd0Z6RVZNQk1HQTFVRUF3d01NVEF1TVRVeUxqRTRNeTR4TUI0WERUSTBNREV5T1RBNE16WXdOMW9YRFRNMApNREV5TmpBNE16WXdOMW93RnpFVk1CTUdBMVVFQXd3TU1UQXVNVFV5TGpFNE15NHhNSUlCSWpBTkJna3Foa2lHCjl3MEJBUUVGQUFPQ0FROEFNSUlCQ2dLQ0FRRUFramhtOGdzTmR1ZGZtVEdxbG92cUMwV3J1SmtjWGtVSWhVY2MKd1VyYitydC9HNHowRXlUcitoZ3h4TWFVbE1MVkVTdVl6NUc3QU1ONlZEKzdEeWNYYW1HYWNKbVNBc2pQSE9oVQpnUHdmbnBuVXR3aENNVEZPY2ZkdHdNUHBEZzBqa2g0SkN3K3Z1R2NnME1aTGRiRFNzUDlLZ2JMejIyaDZhUWwyCjJCUGJ4c08xM0VmYlJaUG9abVc5cXVqaXZtd0NLblhBRHVYalNadnlxYi9TSGd3RFZYTkVpWGNaYmliNGxWQ3YKQXQ2amxOQjc1anZXRjNvRWozZzJTbncxQUNBbitqZSs1NVNWajBMeFNYcjdYeTlPcVpYY0lKL3B1cnEzZ2tGeAo2VGdMQlIzZko3dFhrMk9mU3djaUxEVFl0WEphbDQwUWQxY2YxbFBSZW9WbGJFWkxld0lEQVFBQm8xTXdVVEFkCkJnTlZIUTRFRmdRVXRTNWdjTCtYUEZ1MHkzK2xXVy9PMXN1VGYyNHdId1lEVlIwakJCZ3dGb0FVdFM1Z2NMK1gKUEZ1MHkzK2xXVy9PMXN1VGYyNHdEd1lEVlIwVEFRSC9CQVV3QXdFQi96QU5CZ2txaGtpRzl3MEJBUXNGQUFPQwpBUUVBVE5GWktzbHBXREtFN1hxRW5BaWx1SEI1TE9UZ0ZsdEx3TGV1enorK2sraGxNcWdmUVdadkxnWHd4d2pXCnBpWUtOYTVmWVk2REtDdS9McGgvV0RnQk0wSEtuMG45RkRhaEo4R1pMTHRHRVZiRjUzSGdpdTBIb0l4eTJkTWIKcFE5T012R1YydG54bWFEeG0xbmJ2Ykp1ZG9xcFN2YXFOdHJKVVdlR1cvZndnZm5wNDBsQVJBUEh4NEM0aWswQQpRSUpUY1I2TmZZaDJ2bmo0d2lWV1ZBT1k3K2NkQjJ5QW5JaTFxUENiVnlXa2tBZnR3Mm1BSkJoRWRnN0cxSHBxCm5waGdab2ZyZkdrQlVzL2xpcVY0VEpJWnpJRDJjTFdwRzZ5U09JVStsWWlQcXhkcHRxRnRoeE5oTkNoalRBSmcKOHd3bFMyWE1ueXlOSDAwTlVGWnkwc09CUGc9PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==', serverUrl: 'https://172.20.5.66:16443') {
    // some block

         stage('Deploy Nginx YAML File') {
                  sh 'kubectl apply -f nginx-deployment.yaml'
                  // sh 'kubectl get pod'
                                    }
}
      #kubeconfig(caCertificate: '''-----BEGIN CERTIFICATE-----
MIIBiDCCAS6gAwIBAgIBADAKBggqhkjOPQQDAjA7MRwwGgYDVQQKExNkeW5hbWlj
bGlzdGVuZXItb3JnMRswGQYDVQQDExJkeW5hbWljbGlzdGVuZXItY2EwHhcNMjEw
MzI0MDUwNzA2WhcNMzEwMzIyMDUwNzA2WjA7MRwwGgYDVQQKExNkeW5hbWljbGlz
dGVuZXItb3JnMRswGQYDVQQDExJkeW5hbWljbGlzdGVuZXItY2EwWTATBgcqhkjO
PQIBBggqhkjOPQMBBwNCAARMO7Ag8armJKKvhRcxCsHp1+oWwLiHoY7krAeOjVca
hzXGQu5zaAQyRvgvE8TElXvTVJV6GuFUpAfMqCcA/k8YoyMwITAOBgNVHQ8BAf8E
BAMCAqQwDwYDVR0TAQH/BAUwAwEB/zAKBggqhkjOPQQDAgNIADBFAiEA6cmHVpNu
1oURR8FBKm46uldAVG8/iqed05X5Ob0VXXQCIDpXcbQUussfetNfmHb65hwc/2tW
P9V/xvyOokeKAvZd
-----END CERTIFICATE-----''', credentialsId: 'Rancher_Login', serverUrl: 'https://203.151.50.20/k8s/clusters/c-bfhk6') {
 #   // some block
         #   stage('Deploy Nginx YAML File') {
         #         sh 'kubectl apply -f nginx-deployment.yaml'
         #         // sh 'kubectl get pod'
         #                           }
            } 
                         }
    
         }
    }
        }
    }
  }
}
