pipeline {
    agent any
    environment {
        IMAGE_NAME = "react-app"
        CONTAINER_NAME = "react-container"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Pavandkurdekar/containerized-react-ci-cd'
            }
        }
        stage('Install & Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Stop Old Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }
        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 80:80 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }
}
