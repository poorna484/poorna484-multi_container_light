pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    environment {
        REPO_URL = "https://github.com/poorna484/poorna484-multi_container_light.git"
        BRANCH = "main"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Stop Old Containers') {
            steps {
                sh 'docker compose down || true'
            }
        }

        stage('Run Containers') {
            steps {
                sh 'docker compose up -d'
            }
        }

        stage('Clean Docker Images') {
            steps {
                sh 'docker image prune -f'
            }
        }

    }
}
