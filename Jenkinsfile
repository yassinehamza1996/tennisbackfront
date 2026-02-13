pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Clean') {
            steps {
                bat 'mvn clean'
            }
        }

        stage('Build & Test') {
            steps {
                // Build the Spring Boot jar
                bat 'mvn install -DskipTests'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn sonar:sonar'
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
                // Ensure Docker context is correct and jar exists
                bat 'docker-compose build'
                bat 'docker-compose up -d'
            }
        }
    }
}
