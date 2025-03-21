pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
               sh '''
                    echo "Inside Build stage"
                    ls -la
                    node -v
                    npm -v
                    npm ci
                    npm run build
                    ls -la
               '''
            }
        }
        stage('Test') {
            steps {
               sh '''
                    echo "Inside Test stage"
                    test -f build/index.html
               '''
            }
        }
        
    }
}
