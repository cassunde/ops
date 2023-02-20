pipeline {
    agent any

    stages {
        stage('Build') {
            agent { docker 'adoptopenjdk/openjdk11:jdk-11.0.9.1_1' }
            steps {
                sh 'java -version'
            }
        }
        stage('Docker Build') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Docker Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}