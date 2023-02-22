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
            agent { docker 'adoptopenjdk/openjdk11:jdk-11.0.9.1_1' }
            steps {
                sh './mvnw package'
            }
        }
        stage('Docker Build') {
            agent any
            steps {
                script {
                    dockerImage = docker.build "inlinesoft/ops:0.0.$BUILD_NUMBER"                   
                }
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