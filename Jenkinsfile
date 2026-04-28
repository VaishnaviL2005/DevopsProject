pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    environment {
        IMAGE_NAME = "devforum-app:latest"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Prisma Generate') {
            steps {
                sh 'npx prisma generate'
            }
        }

        stage('Build Project') {
            steps {
                sh 'npm run build'
            }
        }

        // 🔥 Build Docker Image
        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        // 🔥 Load image into Minikube
        stage('Load Image to Minikube') {
            steps {
                sh 'minikube image load $IMAGE_NAME .'
            }
        }

        // 🚀 Deploy to Kubernetes
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yml'
                sh 'kubectl apply -f service.yml'
            }
        }

        // ⚡ Apply Autoscaling
        stage('Apply HPA') {
            steps {
                sh 'kubectl autoscale deployment devforum-deploy --cpu=50% --min=1 --max=5 || true'
            }
        }

        // ✅ Verify Deployment
        stage('Verify Deployment') {
            steps {
                sh 'kubectl get pods'
                sh 'kubectl get svc'
                sh 'kubectl get hpa'
            }
        }

        // 🔄 Ensure rollout success
        stage('Rollout Status') {
            steps {
                sh 'kubectl rollout status deployment/devforum-deploy'
            }
        }
        post {
            success { echo 'Pipeline Successful' }
            failure { echo 'Pipeline Failed' }
        }
    }
}