pipeline {
    agent any
    
    environment {
        NODEJS_HOME = tool name: 'NodeJS_12'
        PATH = "${env.NODEJS_HOME}/bin:${env.PATH}"
        CODECLIMATE_REPO_TOKEN = credentials('codeclimate-repo-token')
    }
    
    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the React application...'
                    sh 'npm install'
                    sh 'npm run build'
                }
            }

        }
        
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    sh 'npm test -- --coverage'
                }
            }

        }
        
        stage('Code Quality Analysis') {
            steps {
                script {
                   // Install CodeClimate test reporter
                    sh 'npm install --save-dev codeclimate-test-reporter'

                    // Run tests with coverage and output coverage report to console
                    sh './node_modules/.bin/codeclimate-test-reporter coverage -t simplecov'

                    // Upload coverage report to CodeClimate
                    sh './node_modules/.bin/codeclimate-test-reporter upload-coverage --input ./coverage/lcov.info --token=${params.CODECLIMATE_REPO_TOKEN}'
                }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying the application...'
                    // Deployment logic here
                }
            }
        }
        
        stage('Release') {
            steps {
                script {
                    echo 'Releasing the application...'
                    // Release logic here
                }
            }
        }
    }
}