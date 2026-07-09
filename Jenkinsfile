pipeline {
    agent any

    environment {
        IMAGE_NAME = "trivy-demo"
        IMAGE_TAG  = "1.0"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/raheebmubarak/Pipeline-trivy-scan.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME:$IMAGE_TAG .
                '''
            }
        }

        stage('Trivy Image Scan') {
            steps {
                sh '''
                trivy image \
                  --scanners vuln \
                  --severity HIGH,CRITICAL \
                  $IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }
    }

    post {
        always {
            sh 'docker images'
        }
    }
}
