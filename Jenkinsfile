pipeline {
    agent any

    environment {
        DOCKERHUB_USER = 'cherry3104'
        DOCKERHUB_PASS = credentials('dockerconnection) // stored in Jenkins
        IMAGE_NAME = 'trendproject/trent-react-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Selvam3195/Trendproject.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${Trend_react_app}:${latest} ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh "echo ${DOCKERHUB_PASS} | docker login -u ${cherry3104} --password-stdin"
                sh "docker push ${trent_react_app}:${latest}"
                sh "docker tag ${cherry3104}:${latest} ${trend_react_app}:latest"
                sh "docker push ${cherry3104/trend_react_app}:latest"
            }
        }
    }

    post {
        success {
            echo "Build & Push successful: ${cherry3104/trend_react_app}:latest"
        }
        failure {
            echo "Build failed."
        }
    }
}
