pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-21-openjdk-amd64'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Verify Java') {
            steps {
                sh 'echo JAVA_HOME=$JAVA_HOME'
                sh 'java -version'
                sh 'javac -version'
                sh 'mvn -v'
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
