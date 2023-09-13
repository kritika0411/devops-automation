pipeline {
    agent any
    tools{
       maven 'MAVEN'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kritika0411/devops-automation.git']])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t kritz4/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'docker-reg-jenkins', variable: 'docker-reg-jenkins')]) {
                   bat 'docker login -u kritz4 -p ${docker-reg-jenkins}'

}
                   bat 'docker push kritz4/devops-integration'
                }
            }
        }
        
    }
}
