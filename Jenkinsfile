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
                sh "docker build -t ${trend_react_app}:${latest}"
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
            stage('Deploy to EKS') {
            steps {
                sh '''
                echo "Updating kubeconfig for EKS..."
                aws eks update-kubeconfig --region $ap-south-1 --name $my-eks-cluster2

                echo "Deploying to Kubernetes..."
                kubectl apply -f deployment.yml
                kubectl apply -f service.yml
                '''
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
