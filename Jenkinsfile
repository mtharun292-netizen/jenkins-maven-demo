pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    triggers {
        githubPush()
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Unit Test') {
            steps {
                sh 'echo "Running unit tests (mock stage)"'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                  docker build -t hello-app:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Deploy (Mock)') {
            steps {
                sh '''
                  echo "Deploying hello-app:${BUILD_NUMBER}"
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build & pipeline successful'
        }
        failure {
            echo '❌ Build failed – investigate logs'
        }
    }
}
