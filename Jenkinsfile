pipeline {
  agent { label 'docker_host' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('djay1720')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t djay1720/k8proj:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
      }
    }
    stage('Push') {
      steps {
        sh 'docker push djay1720/k8proj:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
