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
                    // Prepare CodeClimate test reporter
                    sh './node_modules/.bin/codeclimate-test-reporter before-build'

                    // Run tests with coverage
                    sh 'npm test -- --coverage'

                    // Upload coverage report to CodeClimate
                    sh './node_modules/.bin/codeclimate-test-reporter after-build --exit-code $?'
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