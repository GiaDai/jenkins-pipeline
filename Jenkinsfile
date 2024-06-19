pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'nodejs-app:latest'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Build Docker image from the source code
                    sh 'docker build -t nodejs-app:latest .'
                }
            }
        }
        
        stage('Push to Local Registry') {
            steps {
                script {
                    // Save the Docker image as a tar file
                    sh 'docker save nodejs-app:latest -o nodejs-app.tar'
                    
                    // Load the Docker image into Minikube's Docker daemon
                    sh 'minikube ssh "docker load < /path/to/nodejs-app.tar"'
                }
            }
        }

        stage('Deploy to Minikube') {
            steps {
                script {
                    // Apply the Kubernetes deployment configuration
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}
