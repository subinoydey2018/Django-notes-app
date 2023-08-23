pipeline {
    agent any
    
    stages{
        stage("Pull"){
            steps {
                echo "Code will replica from github"
                git url: "https://github.com/subinoydey2018/Django-notes-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Code will build here"
                sh "docker build -t notes-app ."
            }  
        }
        stage("Push to Docker Hub"){
            steps {
                echo "After build it will push to Docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub", passwordVariable:"dockerhubpass", usernameVariable:"dokerhubid")]){
                sh "docker tag notes-app ${env.dokerhubid}/new-note-app"
                sh "docker login -u ${env.dokerhubid} -p ${env.dockerhubpass}"
                sh "docker push ${env.dokerhubid}/new-note-app"
                }
            }    
        }
        stage("Deploy"){
            steps {
                echo "After build apps will push to container"
                sh "docker-compose down && docker-compose up -d"
            }  
        }
    }
}
