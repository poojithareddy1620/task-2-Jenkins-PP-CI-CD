pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-demo-app"
        DOCKER_HUB_USER = "your_dockerhub_username"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/poojithareddy1620/task-2-Jenkins-PP-CI-CD.git'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-password', variable: 'DOCKER_PASSWORD')]) {
                    sh '''
                        echo $DOCKER_PASSWORD | docker login -u $DOCKER_HUB_USER --password-stdin
                        docker tag $IMAGE_NAME $DOCKER_HUB_USER/$IMAGE_NAME
                        docker push $DOCKER_HUB_USER/$IMAGE_NAME
                        docker logout
                    '''
                }
            }
        }
    }
}  
