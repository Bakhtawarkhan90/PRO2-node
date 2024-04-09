pipeline {
    agent any 

    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/Bakhtawarkhan90/PRO2-node.git", branch: "master"
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
                    sh 'docker tag pro2 ${dockerHubUser}/pro2:latest'
                    sh 'docker login -u ${dockerHubUser} -p "${dockerHubPass}"'
                    sh 'docker push ${dockerHubUser}/pro2:latest'
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker run -d -p 8000:8000  pro2:latest "
            }
        }
    }
}
