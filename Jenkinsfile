pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerconnection')
        IMAGE_NAME = "cherry3104/trend_react_app"
        IMAGE_TAG = "latest"
        AWS_REGION = "ap-south-1"
        EKS_CLUSTER = "my-eks-cluster3"
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
                sh "docker build -t trent-react-app ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerconnection', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                    echo "Updating kubeconfig for EKS..."
                     aws eks update-kubeconfig --region ${AWS_REGION} --name ${EKS_CLUSTER}
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker push ${IMAGE_NAME}:${IMAGE_TAG}
                    """
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh """
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
