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
        stage('Build') {
            steps {
                sh 'echo "Hello world!"'
                sh 'node --version'
                sh 'npm --version'
                sh 'npm config set registry https://registry.npm.taobao.org'
                sh 'npm install'
            }
        }
        stage('Test'){
            steps{
                sh './jenkins/scripts/test.sh'
            }
        }
    }
}
