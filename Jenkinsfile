pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t DOCKER_USER/ci-cd-demo:latest .'
      }
    }

    stage('Push to Docker Hub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh """
            echo $PASS | docker login -u $USER --password-stdin
            docker push $USER/ci-cd-demo:latest
          """
        }
      }
    }
  }
}
