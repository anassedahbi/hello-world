pipeline {
    agent any
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
                        sh 'mvn clean package'
                    } catch (Exception e) {
                        echo "Error during Maven build bro"
                        throw e
                    }
                }
            }
        }
        stage('List Generated Files') {
            steps {
                sh 'ls -l target'
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
