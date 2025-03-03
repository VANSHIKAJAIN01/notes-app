pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/VANSHIKAJAIN01/notes-app.git'
            }
        }
        stage('Docker Build') {
            steps {
                echo 'Pretending to build Docker image...'
            }
        }
        stage('Push to DockerHub') {
            steps {
                echo 'Pretending to push Docker image...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Pretending to deploy the app...'
            }
        }
    }
}
