pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t microservice-app:latest .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run -d -p 5000:5000 microservice-app'
                sh 'curl -f http://localhost:5000 || exit 1'
            }
        }
        stage('Push to Registry') {
            steps {
                sh 'docker tag microservice-app:latest Vetri/microservice-app:latest'
                sh 'docker push Vetri/microservice-app:latest'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
