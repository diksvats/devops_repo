pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('diksha_vats_')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/diksvats/devops_repo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t dikshavats/newimage:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push dikshavats/newimage:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
