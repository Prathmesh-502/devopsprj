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
        script {
          docker.build("workshop-site:${env.BUILD_NUMBER}")
        }
      }
    }
    stage('Run Docker Container') {
      steps {
        script {
          sh 'docker stop workshop-site || true'
          sh 'docker rm workshop-site || true'
          sh 'docker run -d -p 8082:80 --name workshop-site workshop-site:${env.BUILD_NUMBER}'
        }
      }
    }
  }
}
