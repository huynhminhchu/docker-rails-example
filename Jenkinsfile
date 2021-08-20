pipeline {
    agent { label 'linux' }
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker-compose build'
            }
        }
        stage('Deploy to staging') {
            steps {
                sh 'docker-compose up'
                sleep 30
                sh './run rails db:setup'
            }
        }
        stage('Test'){
            steps {
                sh 'echo $(curl localhost:8000)'
            }
        }
    }   
}
