pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerconnection')
        IMAGE_NAME = "trendproject/trent-react-app"
        IMAGE_TAG = "latest"
        AWS_REGION = "ap-south-1"
        EKS_CLUSTER = "my-eks-cluster"
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
                sh "docker build -t ${trendproject/trent-react-app}:${latest} ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerconnection', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker push ${trendproject/trent-react-app}:${latest}
                    """
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                echo "Deploying to Kubernetes..."
                kubectl apply -f deployment.yml
                kubectl apply -f service.yml
                """
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
