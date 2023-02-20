pipeline {
    agent any

    stages {
        stage('Build') {
            agent { docker 'adoptopenjdk/openjdk11:jdk-11.0.9.1_1' }
            steps {
                sh './mvnw package'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build "inlinesoft/ops:0.0.$BUILD_NUMBER"                   
                }
            }
        }
        stage('Docker Deploy') {
            steps {
                script {
                    docker.withRegistry( 'https://registry-1.docker.io', 'docker_hub' ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}