pipeline {
    agent { label 'linux' }
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker-compose build'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
                sleep 5
            }
        }
        stage('Set up the initial DB'){
            steps {
                sh './run rails db:setup'
            }
        }
        stage('Test'){
            steps {
                sh './run rails test'
                sh 'echo $(curl localhost:8000)'
            }
        }
    }
    post {
        always {
            sh 'docker-compose down'
        }
    }
     
}
