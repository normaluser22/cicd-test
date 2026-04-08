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
                // 한 줄의 쉘 스크립트로 파일 생성 및 내용 기록
                sh 'echo "git clone end" > cicd_test.txt'
            }
        }
    }
} // pipeline 블록 닫기
