pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build/compile application'
                sh 'ls'
            }
        }
        stage('Test') {
            steps {
                echo 'Test run application'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy to server'
            }
        }
    }
}
