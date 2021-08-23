pipeline {
    agent { label 'linux' }
    parameters {
        string(name: 'WAIT_TIME', defaultValue: '5', description: 'How long should i wait?')
    }
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker-compose build'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
                
            }
            post { 
                success {
                    echo 'This is post stage'
                    sleep ${params.WAIT_TIME}
                }
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
