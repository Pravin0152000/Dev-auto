pipeline {
    agent any 
    tools {
        maven 'Maven_3.9.6'
    }
    stages{
        stage('checking into git hub'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Java-Techie-jt/devops-automation']])
                bat 'mvn clean install'
            }
        }
        stage('building docker image'){
            steps{
                script{
                    bat 'docker build -t pravin052000/devops-integration .'
                }
            }
        }
        stage('Pushing into docker hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'Dockerhubcred')]) {
                    bat 'docker login -u pravin052000 -p %Dockerhubcred%'
}
                    
                    bat 'docker push pravin052000/devops-integration'
                }
            }
        }
    }
}