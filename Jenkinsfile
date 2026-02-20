pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t hello-app:1.0 .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                  docker rm -f hello-app || true
                  docker run -d --name hello-app hello-app:1.0
                '''
            }
        }
    }
}
