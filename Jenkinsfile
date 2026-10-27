pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Manas0667/jenkins-docker-webapp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t manasvarshney/webapp:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo "$PASS" | docker login -u "$USER" --password-stdin'
                    sh 'docker push manasvarshney/webapp:latest'
                    sh 'docker logout'
                }
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'docker pull manasvarshney/webapp:latest'
                sh 'docker stop webapp-container || true'
                sh 'docker rm webapp-container || true'
                sh 'docker run -d --name webapp-container -p 8083:80 manasvarshney/webapp:latest'
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}