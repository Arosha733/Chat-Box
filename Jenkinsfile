pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'your-docker-image'
        STAGING_SERVER = 'localhost'  // Using local machine as staging
        PRODUCTION_SERVER = 'localhost'  // Using local machine as production
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    // Run Docker container for staging environment
                    sh 'docker run -d --name staging-container -p 8080:80 $DOCKER_IMAGE'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    // Run integration tests here
                    sh './test.sh'
                }
            }
        }
        stage('Approve Production Deployment') {
            steps {
                script {
                    // Manual approval step for production deployment
                    input 'Approve Production Deployment'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    // Run Docker container for production environment
                    sh 'docker run -d --name production-container -p 9090:80 $DOCKER_IMAGE'
                }
            }
        }
    }
}
