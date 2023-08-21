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
                stash name: 'GOAPP', includes: 'applib'
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
                sh 'curl http://localhost:8081/api'
                sh 'echo $?'
            }
        }
        stage('Deploy') {
            environment {
                SSH_PRIVATE_KEY = credentials('golang-server-private-key')
            }
            steps {
                echo 'Deploy to server'
                sh 'ls'
                unstash name: 'GOAPP'
                sh 'ls'
                sh 'ssh -o StrictHostKeyChecking=no -i "$SSH_PRIVATE_KEY" adhithia@34.101.194.246 rm -rf applib'
                sh 'scp -o StrictHostKeyChecking=no -i "$SSH_PRIVATE_KEY" applib adhithia@34.101.194.246:~/applib'
                sh 'ssh -o StrictHostKeyChecking=no -i "$SSH_PRIVATE_KEY" adhithia@34.101.194.246 sudo systemctl restart applib'
            }
        }
    }
    post { 
        always { 
            cleanWs()
        }
        success {
            discordSend description: "Success deploy golang app", footer: "Jenkins", link: env.BUILD_URL, result: currentBuild.currentResult, title: JOB_NAME, webhookURL: "https://discordapp.com/api/webhooks/1086510252838633472/VBOt5DABR6XyKwzQbFbUHbYy9r5D_MOny2Q6PjOiaJDl-u_RZpiJe_I2bHce5jSzpM-T"
        }
        failure {
            discordSend description: "Failure deploy golang app", footer: "Jenkins", link: env.BUILD_URL, result: currentBuild.currentResult, title: JOB_NAME, webhookURL: "https://discordapp.com/api/webhooks/1086510252838633472/VBOt5DABR6XyKwzQbFbUHbYy9r5D_MOny2Q6PjOiaJDl-u_RZpiJe_I2bHce5jSzpM-T"
        }
    }
}
