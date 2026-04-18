pipeline {
    agent any

    environment {
        JAVA_HOME = '/opt/jdk-25'
        PATH = "$JAVA_HOME/bin:$PATH"
    }

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
        success {
            echo 'CI pipeline succeeded!'
        }
        failure {
            echo 'Build failed, please check the logs.'
        }
    }
}