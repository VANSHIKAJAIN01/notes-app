pipeline {
    agent any

    environment {
        IMAGE_NAME = "django_app"
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
                    // Build the Docker image with the name used in docker-compose.yaml
                    dockerImage = docker.build("${IMAGE_NAME}:${BUILD_NUMBER}")
                }
            }
        }
        stage('Container Vulnerability Scan - Trivy') {
            steps {
                script {
                    sh '''
                        docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
                        aquasec/trivy image ${IMAGE_NAME}:${BUILD_NUMBER}
                    '''
                }
            }
        }
        stage("Push to DockerHub") { 
            steps {
                withDockerRegistry([credentialsId: 'dockerHubCreds', url: '']) {
                    // Tag the same build to push to DockerHub
                    sh "docker tag ${IMAGE_NAME}:${BUILD_NUMBER} vanshikajain01/notes-app:latest"
                    sh "docker push vanshikajain01/notes-app:latest"
                }
            }
        }
        stage("Deploy") {
            steps {
                sh "echo Deploying the application..."
                
                // Stop and remove existing containers (optional cleanup)
                sh "docker-compose -f docker-compose.yaml down || true"
                
                // Pull the latest image (optional if using local build)
                sh "docker pull vanshikajain01/notes-app:latest"
                
                // Replace the image in docker-compose temporarily or dynamically if needed
                sh '''
                    sed -i '' 's|image: django_app|image: vanshikajain01/notes-app:latest|' docker-compose.yaml
                '''

                // Deploy with docker-compose
                sh "docker-compose -f docker-compose.yaml up -d --build"
            }
        }
    }
}
