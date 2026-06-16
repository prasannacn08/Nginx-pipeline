pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/prasannacn08/Nginx-pipeline.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                    echo "Running SonarQube Analysis..."
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nginx-devops-app .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop nginx || true
                docker rm nginx || true
                docker run -d -p 80:80 --name nginx nginx-devops-app
                '''
            }
        }
    }
}
