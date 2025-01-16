pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Arosha733/Chat-Box.git'
            }
        }
        // Remove the Docker build step if not needed
        // stage('Build') {
        //     steps {
        //         echo 'Building Docker containers...'
        //         bat 'docker build -t your-image-name .'
        //     }
        // }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
    }
}
