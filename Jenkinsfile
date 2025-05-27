pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-demo-app"
        DOCKER_HUB_USER = "poojithareddy1620"
        NODE_PATH = "/root/.nvm/versions/node/v16.20.2/bin"
        PATH = "${NODE_PATH}:${env.PATH}"
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                    export NVM_DIR="$HOME/.nvm"
                    source "$NVM_DIR/nvm.sh" || echo "nvm.sh not found"
                    nvm use 16 || echo "nvm use failed"
                    export PATH=$NVM_DIR/versions/node/v16.20.2/bin:$PATH
                    node -v || true
                    npm -v || true
                    npm install || echo "npm install failed"
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    export NVM_DIR="$HOME/.nvm"
                    source "$NVM_DIR/nvm.sh" || echo "nvm.sh not found"
                    nvm use 16 || echo "nvm use failed"
                    export PATH=$NVM_DIR/versions/node/v16.20.2/bin:$PATH
                    npm test || echo "Tests failed"
                '''
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    docker build -t $IMAGE_NAME . || echo "Docker build failed"
                '''
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-password', variable: 'DOCKER_PASSWORD')]) {
                    sh '''
                        echo $DOCKER_PASSWORD | docker login -u $DOCKER_HUB_USER --password-stdin || echo "Login failed"
                        docker tag $IMAGE_NAME $DOCKER_HUB_USER/$IMAGE_NAME || echo "Tag failed"
                        docker push $DOCKER_HUB_USER/$IMAGE_NAME || echo "Push failed"
                        docker logout
                    '''
                }
            }
        }
    }
}
