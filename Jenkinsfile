pipeline {
    agent any

    stages {
        stage("Code clone") {
            steps {
                sh "whoami"
                git branch: 'main', url: 'https://github.com/VANSHIKAJAIN01/django-notes-app.git'
            }
        }
        stage("Code Build") {
            steps {
                sh "docker build -t notes-app:latest ."
            }
        }
        stage("Push to DockerHub") { 
            steps {
                withDockerRegistry([credentialsId: 'dockerHubCreds', url: '']) {
                    sh "docker tag notes-app:latest vanshikajain01/notes-app:latest"
                    sh "docker push vanshikajain01/notes-app:latest"
                }
            }
        }
        stage("Deploy") {
            steps {
                sh "echo Deploying the application..."
                sh "docker run -d -p 8000:8000 vanshikajain01/notes-app:latest"
            }
        }
    }
}
