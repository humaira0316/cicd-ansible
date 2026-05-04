pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Verify Docker') {
            steps {
                sh 'docker --version'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cicd-ansible-poc:latest .'
            }
        }

        stage('Run Container (Smoke Test)') {
            steps {
                sh '''
                docker rm -f cicd-ansible-test || true
                docker run -d -p 8085:80 --name cicd-ansible-test cicd-ansible-poc:latest
                '''
            }
        }
    }
}

