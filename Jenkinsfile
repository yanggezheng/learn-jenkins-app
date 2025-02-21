pipeline{
    agent any
    environment{
        NETLIFY_SITE_ID = 'a16e31f3-eb03-4231-9537-25bca8ba218b'
    }
    stages{
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
                node --version
                npm --version
                npm ci
                npm run build
                ls -la
                '''
            }
        }
        stage('Test'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                    }
                }
            steps{
                sh '''
                    test -f build/index.html
                    npm test
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
                    netlify --version
                    echo 'Deploying to production. Site ID: $NETLIFY_SITE_ID'
                '''
            }
        }
    }
}