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
    stage ('Build App') {
      steps {
        script {
         sh 'docker build -t flask-app .'
        }
      }
    }
    stage ('Build Network') {
      steps {
        script {
         sh 'docker network create flask_app_network || true'
        }
      }
    }
// 2 slashes to comment
    stage('Deploy Flask App'){
      steps{
        sh 'docker run -d --name flask-app --network flask_app_network -e YOUR_NAME=Andrew flask-app'
      }
    }
    stage('Deploy nginx App'){
      steps{
        sh 'docker run -d -p 80:80 --network flask_app_network --name nginx --mount type=bind,source=$(pwd)/nginx.conf,target=/etc/nginx/nginx.conf nginx:alpine'
      }
    }
  }
}
