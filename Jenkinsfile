pipeline {
    agent any
    
    environment {
        NODEJS_HOME = tool name: 'NodeJS_12'
        PATH = "${env.NODEJS_HOME}/bin:${env.PATH}"
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
                    echo 'Running code quality analysis...'
                   sh '''
                        npm install -g codeclimate-test-reporter
                        cc-test-reporter before-build
                        npm test -- --coverage
                        cc-test-reporter after-build --exit-code $?
                    '''
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