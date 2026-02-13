pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
             stage('Clean') {
            steps {
                bat 'mvn clean'
            }
        }

        stage('Build & Test') {
            steps {
                bat 'mvn install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn sonar:sonar'
                }
            }
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
