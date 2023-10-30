pipeline {
    agent any

    environment {
        registry = "aymane55/automated-web-app"
        registryCredential = 'dockerhub' 
        buildNumber = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('stage 1 : Build Docker Image') {
            steps {
                script {
                    sh "sudo docker build -t automated-web-app:${buildNumber} ."
                }
            }
        }
        stage('stage 2 : Run Docker Container') {
            steps {
                script {
                    sh "sudo docker run -d -p 3000:3000 automated-web-app:${buildNumber}"
                }
            }
        }
        stage('stage 3 : Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', registryCredential) {
                        sh "sudo docker push ${registry}:${buildNumber}"
                    }
                }
            }
        }
    }
}

