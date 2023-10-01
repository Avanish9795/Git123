pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    docker.build('<your-firstname-pincode>')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    // Push Docker image to registry
                    docker.withRegistry('https://registry.example.com', 'registry-credentials') {
                        docker.image('<your-firstname-pincode>').push()
                    }
                }
            }
        }
        stage('Update Kubernetes Deployment') {
            steps {
                script {
                    // Update Kubernetes deployment
                    sh 'kubectl set image deployment/<your-first-name> <your-first-name>=registry.example.com/<your-dockerhub-username>/<your-firstname-pincode>:latest'
                }
            }
        }
    }
}
