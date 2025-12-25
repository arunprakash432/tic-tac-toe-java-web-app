pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK21'
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

        stage('Docker Build') {
            steps {
                sh 'docker build -t tic-tac-toe .'
            }
        }

        stage('Docker Run') {
            steps {
                sh '''
                docker rm -f tic-tac-toe || true
                docker run -d -p 8081:8080 --name tic-tac-toe tic-tac-toe
                '''
            }
        }
    }
}
