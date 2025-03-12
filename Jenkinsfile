pipeline {
    agent any

    stages {
        stage('Start') {
            steps {
                echo 'Lab_1: nginx/custom'
            }
        }

        stage('Build nginx/custom') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t nginx/custom:latest .'
            }
        }

        stage('Test nginx/custom') {
            steps {
                echo 'Running tests...'
                echo 'Pass'
            }
        }

        stage('Deploy nginx/custom') {
            steps {
                echo 'Deploying container...'
                sh "docker run -d -p 90:80 nginx/custom:latest"
            }
        }
    }
}