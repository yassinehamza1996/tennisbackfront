pipeline {
    agent any

  tools {
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Clean') {
            steps {
                 dir('backend') {
                bat 'mvn clean'
                 }
            }
        }

        stage('Build & Test') {
            steps {
                 dir('backend') {
                // Build the Spring Boot jar
                bat 'mvn install -DskipTests'
                 }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                 dir('backend') {
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
                // Ensure Docker context is correct and jar exists
                bat 'docker-compose build'
                bat 'docker-compose up -d'
            }
        }
    }
}
