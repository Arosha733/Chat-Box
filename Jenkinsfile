pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    if (fileExists('backend/package.json')) {
                        dir('backend') {
                            sh 'npm install'
                        }
                    }
                    if (fileExists('frontend/package.json')) {
                        dir('frontend') {
                            sh 'npm install'
                        }
                    }
                }
            }
        }
        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm run build'
                }
            }
        }
        stage('Test Backend') {
            steps {
                dir('backend') {
                    sh 'npm test'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deployment step (configure as per your environment)'
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution complete'
        }
        success {
            echo 'Build succeeded'
        }
        failure {
            echo 'Build failed'
        }
    }
}
