pipeline {

    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Clone') {
            steps {
                echo 'Cloning repository...'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop myapp || true'
                sh 'docker rm myapp || true'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d \
                  --name myapp \
                  -p 5001:5000 \
                  myapp
                '''
            }
        }
    }
}