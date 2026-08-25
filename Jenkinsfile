pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/bmanisha04/secretsanta-generator.git'
            }
        }

        stage ('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage ('Build Docker Image') {

            steps {
                sh 'docker build -t secretsanta-generator:Latest .'
            }
        }



    }
}