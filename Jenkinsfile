pipeline {
    agent any
    environment {
        // Define the Docker image name
        DOCKER_IMAGE = 'simple-node-app'
    }
    stages {
        stage('Checkout') {
            steps {
                // Check out your code from GitHub
                git 'https://github.com/OmMorecdac/app.js.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using your Dockerfile
                    dockerImage = docker.build("${env.DOCKER_IMAGE}")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    // Run tests inside a temporary Docker container
                    echo 'Running tests...'
                    sh "docker run --rm ${env.DOCKER_IMAGE} npm test"
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Deploy your application by running the container in detached mode
                    echo 'Deploying the application...'
                    sh "docker run -d -p 3000:3000 ${env.DOCKER_IMAGE}"
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution complete.'
        }
    }
}
