pipeline {
    agent any

    stages {
        stage('Github Pull') {
            steps {
                // git pull 단계
                git branch: 'main', url: 'https://github.com/normaluser22/cicd-test.git'
            }
        }

        stage('Git clone end') {
            steps {
                sh 'touch cicd_test.txt'
                sh 'echo "git clone end" > cicd_test.txt'
            }
        }
        stage('Deploy Server') {
            sshagent(credentials:['Deploy-Privatekey']){
                sh "scp -o StrictHostKeyChecking=no index.html ubuntu@52.79.166.126:/var/www/html/"  
            }
        }
    }
}
