pipeline {
  agent { label 'ubuntu-agent' }

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
        sh 'docker login -u djay1720 -p '
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
