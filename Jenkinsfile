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
                   withCredentials([string(credentialsId: 'kritz4', variable: 'cred1')]) {
                   bat 'docker login -u kritz4 -p ${cred1}'

}
                   bat 'docker push kritz4/devops-integration'
                }
            }
        }
        
    }
}
