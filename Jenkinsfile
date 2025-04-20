pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git(
                    url: 'https://github.com/ranjeetchavan7/simple-webapp-docker.git',
                    branch: 'main' // Or 'master', depending on your repository's default branch
                )
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("simple-webapp:${BUILD_ID}", ".")
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any existing container
                    sh 'docker stop my-webapp || true'
                    sh 'docker rm my-webapp || true'

                    // Run the new container and map port 5000 on the container to port 80 on the host
                    dockerContainer = dockerImage.run('-d -p 80:5000 --name my-webapp')
                }
            }
        }
    }
}