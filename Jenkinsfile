pipeline {
    agent any
    environment {
        // Define environment variables (e.g., repository, image names)
        DOCKER_REGISTRY = 'docker.io'  // Change this if you're using a different registry
        IMAGE_NAME = 'your-image-name'
        DOCKER_TAG = 'latest'
        STAGING_SERVER = 'staging-server-url' // Replace with your actual staging server URL
        PRODUCTION_SERVER = 'production-server-url' // Replace with your actual production server URL
    }
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    echo "Checking out the code from GitHub"
                    // Checkout code from GitHub repository
                    git credentialsId: 'your-git-credentials-id', url: 'https://github.com/your-org/your-repo.git'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image..."
                    // Build Docker image
                    docker.build("${IMAGE_NAME}:${DOCKER_TAG}")
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Deploying Docker image to staging..."
                    // Push the Docker image to your registry
                    docker.push("${IMAGE_NAME}:${DOCKER_TAG}")
                    
                    // Deploy Docker container to staging server (use SSH or another method)
                    sh "ssh user@${STAGING_SERVER} 'docker run -d --rm --name ${IMAGE_NAME} ${DOCKER_REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}'"
                }
            }
        }

        stage('Run Integration Tests') {
            steps {
                script {
                    echo "Running integration tests..."
                    // Run your integration tests (e.g., using a testing script)
                    sh './run_integration_tests.sh' // Replace with your actual test command
                }
            }
        }

        stage('Approval for Production Deployment') {
            steps {
                input message: 'Do you want to deploy to production?', ok: 'Deploy to Production'
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploying Docker image to production..."
                    // Deploy Docker container to production server (use SSH or another method)
                    sh "ssh user@${PRODUCTION_SERVER} 'docker run -d --rm --name ${IMAGE_NAME} ${DOCKER_REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}'"
                }
            }
        }
    }

    post {
        success {
            echo "CD Pipeline finished successfully!"
        }
        failure {
            echo "CD Pipeline failed!"
        }
    }
}
