pipeline {
  agent any
  stages {
    stage ('Clean-up') {
      steps {
        script {
          sh 'docker rm -f $(docker ps -a) || True'
          sh 'docker rmi $(docker images) || True'
          sh 'docker volume rm $(docker volume ls) || True'
          sh 'docker builder prune --all --force'
        }
      }
    }
    stage ('Build') {
      steps {
        script {
         sh './buildstage.sh'
        }
      }
    }
// 2 slashes to comment
    stage('Deploy'){
      steps{
       sh './deploystage.sh'
      }
    }
  }
}
