pipeline {
    agent{
        docker{
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    environment{
        CI = 'true'
    }
    stages {
        stage('Start'){
            steps{
                sh 'echo "Hello world!"'
                sh 'node --version'
                sh 'npm --version'
                sh 'npm config set registry https://registry.npm.taobao.org'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test'){
            steps{
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver'){
            steps{
                input message: '是否开启交付服务器?'
                sh './jenkins/scripts/deliver-for-development.sh'
                sh 'echo "交付服务开启了: localhost:3000"'
                input message: '是否关闭交付服务?'
            }
        }
    }
}
