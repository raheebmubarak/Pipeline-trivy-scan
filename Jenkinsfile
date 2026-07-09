pipeline {
    agent any

    environment {
        IMAGE_NAME = "trivy-demo"
        IMAGE_TAG = "latest"
        TRIVY_PATH = "C:\Users\ASUS\AppData\Local\Microsoft\WinGet\Packages\AquaSecurity.Trivy_Microsoft.Winget.Source_8wekyb3d8bbwe\trivy"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/raheebmubarak/Pipeline-trivy-scan.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:%IMAGE_TAG% .'
            }
        }

        stage('Trivy Image Scan') {
            steps {
                bat '"%TRIVY_PATH%" image %IMAGE_NAME%:%IMAGE_TAG%'
            }
        }
    }

    post {
        always {
            bat 'docker images'
        }
    }
}
