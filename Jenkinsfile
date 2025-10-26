pipeline {
    agent any

    tools {
        jdk 'Java17'
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Cloning GitHub repository..."
                git branch: 'main',
                    url: 'https://github.com/Maheshh123/Maven.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building the project (module: demo)..."
                dir('demo') {
                    bat "mvn clean compile"
                }
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                dir('demo') {
                    bat "mvn test"
                }
            }
        }

        stage('Package') {
            steps {
                echo "Packaging Spring Boot app..."
                dir('demo') {
                    bat "mvn package"
                }
            }
        }

        stage('Archive') {
            steps {
                echo "Archiving jar from demo/target..."
                archiveArtifacts artifacts: 'demo/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "✅ Build completed successfully!"
        }
        failure {
            echo "❌ Build failed. Check logs."
        }
    }
}
