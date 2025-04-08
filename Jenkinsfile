pipeline {
    agent any
    
    parameters {
        string(name: 'IMAGE_TAG', defaultValue: 'latest', description: 'Тег для Docker-образу')
        string(name: 'PORT', defaultValue: '80', description: 'Порт для публікації контейнера')
    }

    stages {
        stage('Start') {
            steps {
                echo 'Lab_2: started by GitHub'
            }
        }

        stage('Image build') {
            steps {
                sh "docker build -t prikm:${params.IMAGE_TAG} ."
                sh "docker tag prikm:${params.IMAGE_TAG} chycherska/prikm:${params.IMAGE_TAG}"
                sh "docker tag prikm:${params.IMAGE_TAG} chycherska/prikm:${BUILD_NUMBER}"
            }
        }

        stage('Push to registry') {
            steps {
                withDockerRegistry([credentialsId: "dockerhub_token", url: ""]) {
                    sh "docker push chycherska/prikm:${params.IMAGE_TAG}"
                    sh "docker push chycherska/prikm:${BUILD_NUMBER}"
                }
            }
        }

        stage('Deploy image') {
            steps {
                sh "docker run -d --rm --name prikm_container -p ${params.PORT}:80 chycherska/prikm:${params.IMAGE_TAG}"
            }
        }

        stage('Cleanup') {
            steps {
                sh "docker image prune -f"
            }
        }
    }
}
