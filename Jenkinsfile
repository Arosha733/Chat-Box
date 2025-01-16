pipeline {
    agent any

    environment {
        STAGING_SERVER = 'staging-server-url' // Replace with your actual staging server URL
        PRODUCTION_SERVER = 'production-server-url' // Replace with your actual production server URL
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                script {
                    echo 'Building Docker containers...'
                    // Example build commands
                    sh 'docker build -t my-backend-image ./backend'
                    sh 'docker build -t my-frontend-image ./frontend'
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to Staging Server...'
                    // Replace the command below with the actual deployment command
                    if (isUnix()) {
                        sh 'nohup docker-compose -f docker-compose.staging.yml up -d &'
                    } else {
                        bat 'start docker-compose -f docker-compose.staging.yml up -d'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running Tests...'
                    // Add test commands
                    sh 'docker exec my-backend-container test-command'
                    sh 'docker exec my-frontend-container test-command'
                }
            }
        }
        
        stage('Approve Production Deployment') {
            steps {
                input 'Approve Production Deployment?'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to Production Server...'
                    // Replace the command below with the actual deployment command
                    if (isUnix()) {
                        sh 'nohup docker-compose -f docker-compose.production.yml up -d &'
                    } else {
                        bat 'start docker-compose -f docker-compose.production.yml up -d'
                    }
                }
            }
        }
    }
}
