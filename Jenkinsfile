pipeline {
agent any

```
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
            withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                sh 'echo "$PASS" | docker login -u "$USER" --password-stdin'
                sh 'docker push manasvarshney/webapp:latest'
            }
        }
    }
}
```

}
