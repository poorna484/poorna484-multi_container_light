pipeline {
    agent any

    environment {
        DOCKERHUB_REPO = "yourdockerhubusername/light-multi-app"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/yourrepo/lightweight-multi-container-app.git'
            }
        }

        stage('Build Images') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Run Containers') {
            steps {
                sh 'docker compose up -d'
            }
        }

        stage('Clean Dangling Images') {
            steps {
                sh 'docker image prune -f'
            }
        }
    }
}
