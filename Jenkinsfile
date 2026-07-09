pipeline {
    agent any

    environment {
        IMAGE_NAME = "trivy-app"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:%IMAGE_TAG% .'
            }
        }

        stage('Trivy Image Scan') {
            steps {
                bat 'trivy image %IMAGE_NAME%:%IMAGE_TAG%'
            }
        }
    }

    post {
        always {
            bat 'docker images'
        }
    }
}
