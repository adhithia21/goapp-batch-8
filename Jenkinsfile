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
                sh 'GOCACHE=/tmp/ GOOS=linux GOARCH=amd64 go build -o applib'
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
