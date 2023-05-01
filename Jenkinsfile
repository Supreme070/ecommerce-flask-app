pipeline {
    agent any

    stages {
        stage('Pull code from GitHub') {
            steps {
                git url: 'https://github.com/your_username/ecommerce-flask-app.git'
            }
        }
        stage('Build Docker image') {
            steps {
                sh 'docker build -t your_dockerhub_username/ecommerce-flask-app:latest .'
            }
        }
        stage('Push Docker image') {
            steps {
                sh 'docker login --username your_dockerhub_username --password your_dockerhub_password'
                sh 'docker push your_dockerhub_username/ecommerce-flask-app:latest'
            }
        }
        stage('Deploy to AWS') {
            steps {
                sh '''
                    ssh -o StrictHostKeyChecking=no -i /path/to/your/aws/key.pem ec2-user@your_aws_instance_ip "docker pull your_dockerhub_username/ecommerce-flask-app:latest && docker run -d
                -p 80:5000 --name ecommerce-flask-app your_dockerhub_username/ecommerce-flask-app:latest"
                '''
            }
        }
    }
}
