pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t manilck/duo-jenk:latest -t manilck/duo-jenk:v${BUILD_NUMBER} .
                '''
            }
        }
        stage('Push') {
            steps {
                sh '''
                docker push manilck/duo-jenk:latest
                docker push manilck/duo-jenk:v${BUILD_NUMBER}
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh'''
                kubectl apply -f ./kubernetes
                kubectl set image deployment/flask-deployment flask-container=manilck/duo-jenk:v${BUILD_NUMBER}
                '''
            }
        }
    }
}
