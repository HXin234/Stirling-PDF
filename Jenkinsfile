pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                deleteDir()
                git branch: 'v0.25.0', url: 'https://github.com/Stirling-Tools/Stirling-PDF.git'
                echo 'Successfully checked out Stirling-PDF v0.25.0'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'java -version'
                sh 'chmod +x gradlew'
                sh './gradlew build'
            }
        }

        stage('Test Report') {
            steps {
                junit '**/build/test-results/test/*.xml'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t stirling-pdf:ci-build .'
            }
        }
    }

    post {
        success {
            echo 'CI pipeline succeeded!'
        }
        failure {
            echo 'Build failed, please check the logs.'
        }
    }
}