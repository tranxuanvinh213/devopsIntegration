pipeline {
    agent any
    tools{
        maven 'maven_3.9.5'
    }
    stages{
        stage('Build maven') {
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vinhit213/devopsIntegration']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image') {
            steps{
                script{
                    sh 'docker build -t vinhit213/devops-integration .'
                }
            }
        }
        stage('Push docker image to hub') {
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub_pass', variable: 'dockerhub_pwd')]) {
                        sh 'docker login -u vinhit213  -p ${dockerhub_pwd}'
                    }
                    sh 'docker push vinhit213/devops-integration'

                }
            }
        }
    }
}