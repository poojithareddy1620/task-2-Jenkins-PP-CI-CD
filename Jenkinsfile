pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-demo-app"
        DOCKER_HUB_USER = "poojithareddy1620"
        NVM_DIR = "/var/lib/jenkins/.nvm"
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                    export NVM_DIR="${NVM_DIR}"
                    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
                    nvm use 16
                    node -v
                    npm -v
                    npm install
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    export NVM_DIR="${NVM_DIR}"
                    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
                    nvm use 16
                    npm test
                '''
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
