pipeline {
    agent {
        label 'docker'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Build/compile application'
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
    post { 
        always { 
            cleanWs()
        }
    }
}
