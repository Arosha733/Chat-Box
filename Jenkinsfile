pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'your-image-name'          // Define your Docker image name
        DOCKER_TAG = 'latest'                          // Define Docker tag
        DOCKER_REGISTRY = 'docker.io'                  // Registry to publish the image
        DOCKER_CREDENTIALS = 'Docker-cred'             // Jenkins credentials for Docker Hub
    }

    stages {
        // Stage to checkout the source code
        stage('Checkout') {
            steps {
                git 'https://github.com/Arosha733/Chat-Box.git'
            }
        }

        // Stage to build the Docker image
        stage('Build Docker Image') {
            steps {
                script {
                    // Print the directory structure to verify the location of the requirements.txt file
                    bat 'dir /s requirements.txt'

                    // Build Docker image using Dockerfile
                    bat "docker build -t ${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}:${DOCKER_TAG} ."
                }
            }
        }

        // Stage to login to Docker Hub (or another registry)
        stage('Docker Login') {
            steps {
                script {
                    // Login to Docker using Jenkins credentials (assuming 'Docker-cred' is configured in Jenkins)
                    withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS}", usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        bat 'echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin'
                    }
                }
            }
        }

        // Stage to push the Docker image to a registry
        stage('Push Docker Image') {
            steps {
                script {
                    // Push the image to Docker Hub or the registry defined
                    bat "docker push ${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}:${DOCKER_TAG}"
                }
            }
        }
    }

    post {
        // Cleanup and logout after the build process
        always {
            bat 'docker logout'
        }
    }
}
