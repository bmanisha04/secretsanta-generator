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
                sh 'Build the code'
            }
        }
    }
}