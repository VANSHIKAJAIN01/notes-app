pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/VANSHIKAJAIN01/notes-app.git'
                echo 'Sleeping for 30 seconds...'
                sleep time: 30, unit: 'SECONDS'
            }
        }
        stage('Docker Build') {
            steps {
                echo 'Starting Docker Build...'
                echo 'Sleeping for 60 seconds to simulate a long build...'
                sleep time: 60, unit: 'SECONDS'
                echo 'Docker Build completed.'
            }
        }
        stage('Push to DockerHub') {
            steps {
                echo 'Starting Push to DockerHub...'
                echo 'Sleeping for 45 seconds to simulate upload time...'
                sleep time: 45, unit: 'SECONDS'
                echo 'Push to DockerHub completed.'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Starting Deployment...'
                echo 'Sleeping for 30 seconds to simulate deployment...'
                sleep time: 30, unit: 'SECONDS'
                echo 'Deployment completed.'
            }
        }
    }
}

