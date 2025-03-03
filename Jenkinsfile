pipeline {
    agent any

    environment {
        IMAGE_NAME = "django-app"
    }

    stages {
        stage("Code clone") {
            steps {
                sh "whoami"
                git branch: 'main', url: 'https://github.com/VANSHIKAJAIN01/notes-app.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Container Vulnerability Scan - Trivy') {
            steps {
                script {
                    sh """
                        docker run --rm -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy image ${IMAGE_NAME}:${BUILD_NUMBER}
                    """
                }
            }
        }
        stage("Push to DockerHub") { 
            steps {
                withDockerRegistry([credentialsId: 'dockerHubCreds', url: '']) {
                    sh "docker tag ${IMAGE_NAME}:${BUILD_NUMBER} vanshikajain01/${IMAGE_NAME}:latest"
                    sh "docker push vanshikajain01/${IMAGE_NAME}:latest"
                }
            }
        }
        stage("Deploy") {
            steps {
                sh "echo Deploying the application..."
                sh "docker run -d -p 8000:8000 vanshikajain01/${IMAGE_NAME}:latest"
            }
        }
    }
}
