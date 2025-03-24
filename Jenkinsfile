pipeline {
    agent any
    
    stages {
        stage('Start') {
            steps {
                echo 'Lab_2: started by GitHub' // Виводимо повідомлення про старт
            }
        }
        
        stage('Image build') {
            steps {
                sh "docker build -t prikm:latest ." // Будуємо Docker-образ
                sh "docker tag prikm chycherska/prikm:latest" // Тегуємо останню версію
                sh "docker tag prikm chycherska/prikm:$BUILD_NUMBER" // Тегуємо з номером білду
            }
        }
        
        stage('Push to registry') {
            steps {
                withDockerRegistry([credentialsId: "dockerhub_token", url: ""]) {
                    sh "docker push chycherska/prikm:latest" // Відправляємо останній образ у DockerHub
                    sh "docker push chycherska/prikm:$BUILD_NUMBER" // Відправляємо версію з номером білду
                }
            }
        }
        
        stage('Deploy image') {
            steps {
                sh "docker run -d --restart unless-stopped -p 80:80 chycherska/prikm" // Запускаємо контейнер із автоматичним перезапуском
            }
        }
    }
}
