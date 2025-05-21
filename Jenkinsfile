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
          // Stop and remove any existing container
          sh 'docker stop workshop-site || true'
          sh 'docker rm workshop-site || true'

          // Run the container on port 8083
          sh 'docker run -d -p 8083:80 --name workshop-site workshop-site:' + env.BUILD_NUMBER

          // Echo the local URL
          echo "✅ Application deployed successfully!"
          echo "🌐 Access it at: http://localhost:8083"
        }
      }
    }
  }

  post {
    success {
      echo '🎉 Build and deployment completed.'
    }
    failure {
      echo '❌ Build failed. Check console output for details.'
    }
  }
}
