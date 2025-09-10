pipeline {
  agent none
  environment { IMAGE_NAME = "kartikeyp/flask-hello" }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build (timestamp tag)') {
      agent {
        docker {
          image 'docker:24.0'
          args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
      }
      steps {
        script { env.IMAGE_TAG = sh(script: 'date +%s', returnStdout: true).trim() }
        sh """
          echo "Building: ${IMAGE_NAME}:${IMAGE_TAG}"
          docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
          docker images | grep ${IMAGE_NAME}
        """
      }
    }
  }
}
