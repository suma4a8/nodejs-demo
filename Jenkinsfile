pipeline {
    agent {label "docker-slave"}
    environment {
    DOCKERHUB_CREDENTIALS = credentials('deploy-docker')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/suma4a8/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t sumanth4a8/nodejs:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push sumanth4a8/nodejs:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

