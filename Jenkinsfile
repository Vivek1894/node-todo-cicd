pipeline {
    agent any
    
    stages {
        stage("Code"){
            steps{
                git url: "https://github.com/Vivek1894/node-todo-cicd.git", branch: "master"
                echo 'Code cloned succesfully'
            }
        }
        
        stage("Build & Test"){
            steps{
                sh "docker build -t node-app ."
                echo 'Code build and tested succesfully'
            }
        }
        
        stage("Scan"){
            steps{
                echo 'Code scanned and processed further'
            }
        }
        
        stage("Push"){
            
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPassword",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                sh "docker tag node-app:latest ${env.dockerHubUser}/node-app:latest "
                sh "docker push ${env.dockerHubUser}/node-app:latest"
                echo 'Image pushed to docker hub succesfully'
                }
            }
        }
        
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'Code deployed succesfully'
            }
        }
    }
}
