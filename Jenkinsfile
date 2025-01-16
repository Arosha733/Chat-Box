pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building Docker containers...'
                bat 'docker build -t your-image-name .'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                bat 'docker run -d -p 8080:80 your-image-name'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add your test commands here
                bat 'docker exec your-container-name npm test'
            }
        }
        stage('Approve Production Deployment') {
            steps {
                input message: 'Approve Production Deployment?', ok: 'Deploy'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                bat 'docker run -d -p 80:80 your-image-name'
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
            bat 'docker system prune -f'
        }
    }
}
