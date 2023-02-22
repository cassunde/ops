pipeline {
    agent none
    stages {
        stage('Test') {
            agent { 
                docker {
                    image 'adoptopenjdk/openjdk11:jdk-11.0.9.1_1'
                    reuseNode true
                } 
            }
            steps {
                sh './mvnw test'
            }
        }
        stage('Build') {
            agent { 
                docker {
                    image 'adoptopenjdk/openjdk11:jdk-11.0.9.1_1'
                    reuseNode true
                } 
            }
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
                script {
                    docker.withRegistry( 'https://registry-1.docker.io', 'docker_hub' ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}