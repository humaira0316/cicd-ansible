pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t html-cicd-poc:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f html-cicd || true
                docker run -d -p 8085:80 --name html-cicd html-cicd-poc:latest
                '''
            }
        }
    }
}
