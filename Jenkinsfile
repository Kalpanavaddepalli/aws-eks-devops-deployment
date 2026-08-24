pipeline {
    agent any

    environment {
        AWS_REGION = "us-east-1"
        ECR_REPO = "hello-world-app"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Kalpanavaddepalli/aws-eks-devops-deployment.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app ./app'
            }
        }

        stage('Login to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region $AWS_REGION | \
                docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com
                '''
            }
        }

        stage('Tag Image') {
            steps {
                sh "docker tag my-app:latest ${ECR_URI}:${IMAGE_TAG}"
            }
        }

        stage('Push to ECR') {
            steps {
                sh "docker push ${ECR_URI}:${IMAGE_TAG}"
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                aws eks update-kubeconfig \
                    --region $AWS_REGION \
                    --name hello-eks-cluster

                helm upgrade --install hello-app ./helm-chart/hello-app \
                    --set image.repository=$ECR_URI \
                    --set image.tag=$IMAGE_TAG

                kubectl rollout status deployment/hello-app-deployment
                '''
            }
        }
    }
}
