pipeline {
    agent any

    environment {
        IMAGE_NAME = "kartikeyp/flask-app"
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull latest code
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // dynamic tag = current timestamp
                    def tag = sh(script: "date +%s", returnStdout: true).trim()
                    env.IMAGE_TAG = tag

                    sh """
                    docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                    """
                }
            }
        }

        stage('Show Images') {
            steps {
                sh "docker images | head -n 5"
            }
        }
    }
}
