pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'master',
                credentialsId: 'github-token',
                url: 'https://github.com/Dcode-7/DevopsProject.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
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

    }

    post {
        success {
            echo 'Build completed successfully!'
        }

        failure {
            echo 'Build failed. Check console output.'
        }
    }
}