pipeline {
    agent any
    environment {
        MAVEN_OPTS = "-Dmaven.repo.local=C:/jenkins/.m2/repository"
        DOCKERHUB_USERNAME = "edahbianass273"
        DOCKERHUB_PASSWORD = "GreenBoys2005"
        IMAGE_NAME = "hello-world"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/anassedahbi/hello-world.git'
            }
        }
        stage('Build with Maven') {
            steps {
                script {
                    try {
                        bat 'mvn clean package'
                    } catch (Exception e) {
                        echo "Error during Maven build bro"
                        throw e
                    }
                }
            }
        }
        stage('List Generated Files') {
            steps {
                bat 'dir target'
            }
        }
        stage('Test Docker') {
             steps {
                script {
                        bat 'docker --version'
                        }
                    }
        }
        stage('Docker Build') {
            steps {
                script {
                    try {
                        bat """
                        docker build -t ${DOCKERHUB_USERNAME}/${IMAGE_NAME}:latest .
                        """
                    } catch (Exception e) {
                        echo "Error during Docker build"
                        throw e
                    }
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    try {
                        bat """
                        docker login -u ${DOCKERHUB_USERNAME} -p ${DOCKERHUB_PASSWORD}
                        docker push ${DOCKERHUB_USERNAME}/${IMAGE_NAME}:latest
                        """
                    } catch (Exception e) {
                        echo "Error during Docker push"
                        throw e
                    }
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    try {
                        bat """
                        docker stop hello-world || exit 0
                        docker rm hello-world || exit 0
                        docker run -d -p 8080:8080 --name hello-world ${DOCKERHUB_USERNAME}/${IMAGE_NAME}:latest
                        """
                    } catch (Exception e) {
                        echo "Error running Docker container"
                        throw e
                    }
                }
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
