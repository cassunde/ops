pipeline {
    agent none

    stages {
        stage('Test') {
            agent { docker 'adoptopenjdk/openjdk11:jdk-11.0.9.1_1' }

            steps {
                sh './mvnw test'
            }
        }
        stage('Build') {
            agent any
            steps {
                echo 'Building..'
            }
        }
        stage('Docker Build') {
            agent any
            steps {
                echo 'Testing..'
            }
        }
        stage('Docker Deploy') {
            agent any
            steps {
                echo 'Deploying....'
            }
        }
    }
}