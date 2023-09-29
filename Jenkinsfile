pipeline {
    agent {label "docker-node"}
    environment {
    DOCKERHUB_CREDENTIALS = credentials('sumanth4a8')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/suma4a8/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t nodejs/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push nodejs/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

