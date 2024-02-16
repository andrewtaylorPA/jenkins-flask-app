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
         sh 'echo "Hello"'
        }
      }
    }
// 2 slashes to comment
    stage('Deploy'){
      steps{
       sh 'echo "Hello"'
      }
    }
  }
}
