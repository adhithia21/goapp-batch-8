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
                sh 'ls'
                sh 'GOCACHE=/tmp/ GOOS=linux GOARCH=amd64 go build -o applib'
                sh 'ls'
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'aditirvan/curl:1.0'
                    label 'docker'
                }
            }
            steps {
                echo 'Test run application'
                sh 'ls'
                sh './applib &'
                sh 'curl http://localhost:8080/api'
                sh 'echo $?'
            }
        }
        stage('Deploy') {
            environment {
                SSH_PRIVATE_KEY = credentials('golang-server-private-key')
            }
            steps {
                echo 'Deploy to server'
                sh 'scp -o StrictHostKeyChecking=no -i "$SSH_PRIVATE_KEY" applib adhithia@34.101.194.246:~/applib'
            }
        }
    }
    post { 
        always { 
            cleanWs()
        }
    }
}
