pipeline {
    agent any

    stages {
        stage('Checkout Source Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-cicd-demo:latest .'
            }
        }

        stage('Test Docker Image') {
            steps {
                sh 'docker run --rm jenkins-cicd-demo:latest nginx -t'
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    docker rm -f jenkins-cicd-demo || true

                    docker run -d \
                      --name jenkins-cicd-demo \
                      -p 8081:80 \
                      jenkins-cicd-demo:latest
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
            }
        }
    }
}