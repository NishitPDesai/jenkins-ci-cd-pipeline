pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-simple-app"
        CONTAINER_NAME = "jenkins-simple-app"
        PORT = "3000"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Cleaning workspace and checking out repo..."
                deleteDir() // ensures no leftover files cause Git issues

                // Proper Git checkout
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [],
                    userRemoteConfigs: [[
                        url: 'https://github.com/NishitPDesai/jenkins-ci-cd-pipeline.git'
                    ]]
                ])
            }
        }

        stage('Build') {
            steps {
                echo "Building Docker image..."
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                // Replace this with real tests later
                sh 'echo "All tests passed!"'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying Docker container..."
                // Stop and remove old container if exists
                sh """
                docker ps -q --filter "name=${CONTAINER_NAME}" | grep -q . && docker stop ${CONTAINER_NAME} || true
                docker run -d --rm --name ${CONTAINER_NAME} -p ${PORT}:${PORT} ${IMAGE_NAME}
                """
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
