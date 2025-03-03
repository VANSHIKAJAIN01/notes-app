pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "vanshikajain01/django-notes-app"
        IMAGE_NAME   = "django-notes-app"
        PATH         = "/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:${env.PATH}"
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
                    // Build the Docker image and tag it with the build number.
                    dockerImage = docker.build("${IMAGE_NAME}:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Container Vulnerability Scan - Trivy') {
            steps {
                script {
                    // Run Trivy to scan the newly built image.
                    sh '''
                        docker run --rm -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy image ${IMAGE_NAME}:${BUILD_NUMBER}
                    '''
                }
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
