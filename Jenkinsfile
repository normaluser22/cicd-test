pipeline {
    agent any
    
    environment {
        strDockerImage="normaluser22/cicd-test:0.1"
    }
    stages {
        stage('Github Pull') {
            steps {
                // git pull 단계
                git branch: 'main', url: 'https://github.com/normaluser22/cicd-test.git'
            }
        }

        stage('Docker Image Build') {
            steps {
                script {
                    oDockImage = docker.build(strDockerImage, "-f Dockerfile .")
            }
        }
        stage('Deploy Server') {
            steps {
            sshagent(credentials:['Deploy-Privatekey']){
                sh "scp -o StrictHostKeyChecking=no index.html ubuntu@52.79.166.126:/home/ubuntu/" 
                sh "ssh -o StrictHostKeyChecking=no ubuntu@52.79.166.126 sudo cp /home/ubuntu/index.html /var/www/html"
            }
          }
        }
    }
}
}