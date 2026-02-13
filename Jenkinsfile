pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Stop Containers') {
            steps {
                bat 'docker-compose down'
            }
        }

        stage('Build & Deploy') {
            steps {
                bat 'docker-compose up -d --build'
            }
        }
    }
}
