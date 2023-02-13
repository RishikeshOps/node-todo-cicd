pipeline {
    agent { label 'ironman' }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/RishikeshOps/node-todo-cicd.git', branch: 'master' 
            }
        }
        stage('Build'){
            steps{
                sh 'docker build . -t rishikeshops/todo-app:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'DockerHubPassword', usernameVariable: 'DockerHubUser')]) {
        	     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push rishikeshops/todo-app:latest'
                }
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
