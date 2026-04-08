pipeline {
    agent any

    environment {
        strDockerImage = "normaluser22/cicd-test:0.1"
    }

    stages {
        stage('Github Pull') {
            steps {
                // GitHub 레포지토리에서 메인 브랜치 소스 가져오기
                git branch: 'main', url: 'https://github.com/normaluser22/cicd-test.git'
            }
        }

        stage('Docker Image Build') {
            steps {
                script {
                    // Docker 이미지 빌드 수행
                    oDockImage = docker.build(strDockerImage, "-f Dockerfile .")
                } 
            }
        }

        stage('Docker Image Push') {
            steps {
                script {
                    docker.withRegistry('','docker-auth'){
                        oDockImage.push()
                    }
                }
            }
        }

        stage('Deploy Server') {
            steps {
                sshagent(credentials: ['Deploy-Privatekey']) {
                    sh "scp -o StrictHostKeyChecking=no index.html ubuntu@52.79.166.126:/home/ubuntu/"
                    sh "ssh -o StrictHostKeyChecking=no ubuntu@52.79.166.126 'sudo cp /home/ubuntu/index.html /var/www/html'"
                }
            }
        }
    }
}