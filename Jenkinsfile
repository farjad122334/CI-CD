pipeline {
    agent {label 'runner1'}
    
    triggers {
        githubPush()
    }

    stages {
        stage('Git Checkout') {
            steps {
                git url: 'https://github.com/farjad122334/CI-CD.git' , branch: 'main'
            }
        }
        stage('Clean Old Containers and Images') {
            steps {
                sh '''
                    IMAGE_NAME="organica"

                    # Stop and remove any container using this image
                    CONTAINER_ID=$(docker ps -aq --filter "ancestor=$IMAGE_NAME")
                    if [ -n "$CONTAINER_ID" ]; then
                        echo "Stopping container(s) for image $IMAGE_NAME..."
                        docker stop $CONTAINER_ID || true
                        echo "Removing container(s)..."
                        docker rm $CONTAINER_ID || true
                    fi

                    # Remove existing image
                    IMAGE_ID=$(docker images -q $IMAGE_NAME)
                    if [ -n "$IMAGE_ID" ]; then
                        echo "Removing existing image $IMAGE_NAME..."
                        docker rmi -f $IMAGE_ID || true
                    fi
                '''
            }
        }
        stage('Docker image build') {
            steps {
                sh '''cd  CI-CD
                    docker build -t organica .'''
            }
        }
        stage('Running the service') {
            steps {
                sh 'docker run -d -p 3000:3000 $(docker images -q organica)'
            }
        }
    }
}
