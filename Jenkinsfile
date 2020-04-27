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
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }
    }
}
