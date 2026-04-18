pipeline {
    agent any

    tools {
        jdk 'JDK-25'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Code checkout successful'
            }
        }

        stage('Build & Test') {
            steps {
                bat 'java -version'
                bat 'gradlew.bat build'
            }
        }

        stage('Test Report') {
            steps {
                junit '**/build/test-results/test/*.xml'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t stirling-pdf:latest .'
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