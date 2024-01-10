pipeline {
    agent any
    tools{
        maven 'MAVEN'
    }
    
    environment {     
    DOCKERHUB_CREDENTIALS= credentials('newdockerhub')     
} 
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kritika0411/devops-automation.git']]])
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
                  withCredentials([string(credentialsId: 'newdockerhub', variable: 'newdockerhub')]){
                   bat 'docker login -u kritz4 -p %newdockerhub%'

}
                   bat 'docker push kritz4/devops-integration'
                }
            }
        }
        
    }
}
