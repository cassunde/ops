pipeline {
    agent {docker 'adoptopenjdk/openjdk11:jdk-11.0.9.1_1'}
    stages {
        stage('Test') {            
            steps {
                sh './mvnw test'
            }
        }
        stage('Build') {            
            steps {
                sh './mvnw package'
            }
        }
        stage('Docker Build') {
            agent {
                 label 'master'
             }
            steps {
                script {
                    dockerImage = docker.build "inlinesoft/ops:0.0.$BUILD_NUMBER"                   
                }
            }
        }
        stage('Docker Deploy') {
            agent {
                 label 'master'
             }
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