import java.text.SimpleDateFormat

def TODAY = (new SimpleDateFormat("yyyyMMdd")).format(new Date())

pipeline {
    agent any

    environment {
        strDockerTag="${TODAY}_${BUILD_ID}"
        strDockerImage = "kimsame/cicd-test:${strDockerTag}"
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
                    sh "ssh -o StrictHostKeyChecking=no ubuntu@52.79.166.126 docker container rm -f sampleweb "
                    sh "ssh -o StrictHostKeyChecking=no ubuntu@52.79.166.126 docker run -d -p 80:80 --name sampleweb ${strDockerImage}"
                }
            }
        }
    }
}