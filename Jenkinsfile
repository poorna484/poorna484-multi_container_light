pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    environment {
        REPO_URL = "https://github.com/poorna484/poorna484-multi_container_light.git"
        BRANCH = "main"
        DOCKERHUB_USERNAME = "tejasvi3697"
        IMAGE1 = "service1"
        IMAGE2 = "service2"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub_credential',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Build Images') {
            steps {
                sh 'docker build -t $DOCKERHUB_USERNAME/$IMAGE1 ./service1'
                sh 'docker build -t $DOCKERHUB_USERNAME/$IMAGE2 ./service2'
            }
        }

        stage('Push Images') {
            steps {
                sh 'docker push $DOCKERHUB_USERNAME/$IMAGE1'
                sh 'docker push $DOCKERHUB_USERNAME/$IMAGE2'
            }
        }

        stage('Deploy Containers') {
            steps {
                sh 'docker compose down || true'
                sh 'docker compose up -d'
            }
        }

        stage('Cleanup') {
            steps {
                sh 'docker image prune -f'
            }
        }
    }
}
