pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:23-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    set -e  # fail fast if any command errors

                    echo "Checking environment..."
                    ls -la
                    node --version
                    npm --version

                    echo "Removing old node_modules and package-lock.json..."
                    rm -rf node_modules package-lock.json

                    echo "Downgrading npm to 9.9.0 temporarily..."
                    npm install -g npm@9.9.0 --unsafe-perm=true

                    echo "Installing dependencies cleanly..."
                    npm ci

                    echo "Building the project..."
                    npm run build

                    echo "Listing final artifacts..."
                    ls -la
                '''
            }
        }
    }
}
