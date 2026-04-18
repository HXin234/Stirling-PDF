pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Code checkout successful'
            }
        }

        stage('Build & Test') {
            steps {
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
                sh 'docker build -t stirling-pdf:latest .'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace'
            deleteDir()
        }
        success {
            echo 'Build succeeded!!!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}