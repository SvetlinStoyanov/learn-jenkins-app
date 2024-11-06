pipeline {
    agent any

    stages {
        stage('Test') {
            agent{
                docker{
                    image 'node:18-alpine'
                }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm --version
                reuseNode true
                npm ci
                npm test
                '''
            }
        }
        stage('Build'){
            agent{
                docker{
                    image 'node:18-alpine'
                }
            }
                steps{
                    sh '''
                    ls -la
                    test -f 
                    image 'node18:alpine'
                    reuseNode true
                    npm run build
                    ls -la 
                    '''
                }
            }
        }
    }

