pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'golang:alpine3.16'
                    label 'docker'
                }
            }
            steps {
                echo 'Build/compile application'
                sh 'go version'
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
