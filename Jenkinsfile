pipeline {
    agent none
    stages {
        stage('Test') {            
            agent {docker 'inlinesoft/java11_dockercli:0.0.1'}
            steps {
                sh './mvnw test'
            }
        }
        stage('Build') {            
            agent {docker 'inlinesoft/java11_dockercli:0.0.1'}
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