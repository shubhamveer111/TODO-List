pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/shubhamveer111/TODO-List.git", branch: "main"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t node-app-test-new"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([string(credentialsId: 'dockerhubCred', variable: 'dockerhubCred')]){
                    sh 'docker login docker.io -u shubhamveer111 -p ${dockerhubCred}'
		    echo "Push Docker Image to DockerHub : In Progress"
                    sh "docker tag node-app-test-new shubhamveer111/todo-list:latest"
                    sh "docker push shubhamveer111/todo-list:latest"
		    echo "Push Docker Image to DockerHub : Is Completed"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
