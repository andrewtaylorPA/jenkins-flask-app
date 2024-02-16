pipeline {
  agent any
  stages {
    stage ('Clean-up') {
      steps {
        script {
          sh 'docker rm -f $(docker ps -a) || true'
          sh 'docker rmi $(docker images) || true'
          sh 'docker volume rm $(docker volume ls) || true'
          sh 'docker builder prune --all --force'
        }
      }
    }
    stage ('Build') {
      steps {
        script {
         sh 'docker build -t flask-app .'
        }
      }
    }
// 2 slashes to comment
    stage('Deploy'){
      steps{
        sh 'docker run -d -p 80:80 --name nginx --mount type=bind,source=$(pwd)/nginx.conf,target=/etc/nginx/nginx.conf nginx'
        sh 'docker run -d --name flask-app -e YOUR_NAME=Andrew flask-app
      }
    }
  }
}
