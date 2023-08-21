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
                sh './applib &'
                sh 'curl http://localhost:8080/api'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy to server'
            }
        }
    }
    // post { 
    //     always { 
    //         cleanWs()
    //     }
    // }
}
