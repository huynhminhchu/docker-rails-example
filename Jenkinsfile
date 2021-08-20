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
                sh 'docker-compose run web scripts/wait-for-it.sh db:5432 -- "rake db:create db:migrate"'
                sh 'docker-compose up'
                sleep 60
            }
        }
        stage('Test'){
            steps {
                sh 'echo $(curl localhost:8080)'
            }
        }
    }   
}
