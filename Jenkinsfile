pipeline {
    agent any
    stages{
        stage('Npm install'){
            steps{
                bat 'npm install'
            }
        }

        stage('Build Front'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/GabrielCabreraQ/Tingeso1-kartingrm-frontend']])
                bat 'npm run build'
            }
        }

        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t gabrielcq/kartingrm-frontend:latest .'
                }
            }
        }
        stage('Push image to Docker Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'docker-credentials	', variable: 'password')]) {
                        bat 'docker login -u gabrielcq -p %password%'
                   }
                   bat 'docker push gabrielcq/kartingrm-frontend'
                }
            }
        }
    }
}