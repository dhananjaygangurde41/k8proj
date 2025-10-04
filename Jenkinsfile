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
        echo "Building Docker image..."
        sh 'docker build -t djay1720/k8proj:latest .'
      }
    }

    stage('Login') {
      steps {
        echo "Logging in to Docker Hub..."
        // 🔧 FIX: Added missing quote and corrected syntax
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

    stage('Push') {
      steps {
        echo "Pushing image to Docker Hub..."
        sh 'docker push djay1720/k8proj:latest'
      }
    }
  }

  post {
    always {
      echo "Cleaning up Docker login session..."
      sh 'docker logout'
    }
  }
}
