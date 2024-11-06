pipeline {
    agent any
    
    environment{
        NETLIFY_SITE_ID = "4930ba03-471d-458c-a81f-de2bf1b0b756"
    }

    stages {
        stage('Test') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm --version
                npm ci
                npm test
                '''
            }
        }
        stage('Build'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
                steps{
                    sh '''
                    ls -la
                    test -f 'build/index.html'
                    npm run build
                    ls -la 
                    '''
                }
            }
            stage('Deploy'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
                steps{
                    sh '''
                    npm install netlify-cli 
                    node_modules/.bin/netlify --version
                    echo "Deploying to production. Site id: $NETLIFY_SITE_ID"
                    '''
                }
            }
        }
    }

