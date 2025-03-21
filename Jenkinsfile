pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID='qwer-e4vbnm-8s6-csnck-jncj'
    }

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
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
               sh '''
                    echo "Inside Test stage"
                    test -f build/index.html
                    npm test
               '''
            }
        }
        stage('Deploy') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
               sh '''
                    echo "Inside Deploy stage"
                    npm i netlify-cli
                    node_modules/.bin/netlify --version
                    echo "Deploying to production. Site ID: $NETLIFY_SITE_ID"
                    
                    
               '''
            }
        }
    }
    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
}
