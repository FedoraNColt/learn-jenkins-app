pipeline {
    agent any

    stages {
        stage('w/o docker') {
            steps {
                sh '''
                    echo 'Run without docker'
                    ls -la
                    touch container-no.txt
                '''
            }
        }
        stage('w/ docker') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Run with docker'
                sh '''
                    npm --version
                    ls -la
                    touch container-yes.txt
                '''
            }
            
        }
    }
}