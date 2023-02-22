pipeline {
    agent {
        docker {
            image 'inlinesoft/java11_dockercli:0.0.1'
            args  '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
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