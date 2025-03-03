pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/VANSHIKAJAIN01/notes-app.git'
            }
        }
        stage('Docker Build') {
            steps {
                echo 'Pretending to build Docker image...'
                // no actual docker commands
            }
        }
        stage('Push to DockerHub') {
            steps {
                echo 'Pretending to push Docker image...'
                // no actual push
            }
        }
        stage('Deploy') {
            steps {
                echo 'Pretending to deploy the app...'
                // nothing happens
            }
        }
    }
}
