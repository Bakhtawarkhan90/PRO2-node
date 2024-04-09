pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/Bakhtawarkhan90/PRO2-node.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t pro2 ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag pro2 ${env.dockerHubUser}/pro2:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/pro2:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
