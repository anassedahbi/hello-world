pipeline {
    agent any
    environment {
            MAVEN_OPTS = "-Dmaven.repo.local=C:/jenkins/.m2/repository"
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
                        echo "Error during Maven builddd bro"
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
    }
    post {
        success {
            echo "Build succeeded!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
