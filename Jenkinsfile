pipeline {
    agent any
    tools{
        maven 'maven_3_6_3'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/benneykwag/github-actions-example']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t jaspersys0623/devops-integration .'
                }
            }
        }
        stage('Push image to HUB'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u jaspersys0623@gmail.com -p ${dockerhubpwd}'
                    }
                    sh 'docker push jaspersys0623/devops-integration'
                }
            }
        }
    }
}
