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
          bat 'docker stop workshop-site || exit 0'
          bat 'docker rm workshop-site || exit 0'
          bat "docker run -d -p 8083:80 --name workshop-site workshop-site:%BUILD_NUMBER%"
          echo " App deployed at: http://localhost:8083"
        }
      }
    }
  }

  post {
    success {
      echo ' Build & deployment done!'
    }
    failure {
      echo ' Build failed.'
    }
  }
}
