pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-website:latest .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f devops-nginx || true
                    docker run -d \
                        --name devops-nginx \
                        -p 8081:80 \
                        devops-website:latest
                '''
            }
        }
    }
}
