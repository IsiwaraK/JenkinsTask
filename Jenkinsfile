pipeline {
    agent any
    
    environment {
        NODEJS_HOME = tool name: 'NodeJS_12'
        PATH = "${env.NODEJS_HOME}/bin:${env.PATH}"        
        CODECLIMATE_REPO_TOKEN = credentials('codeclimate-repo-token') // Store your CodeClimate repo token in Jenkins credentials

    }
    
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'npm test -- --coverage'
                }
            }
        }
        stage('Code Quality Analysis') {
            steps {
                script {
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
                    echo 'Deploy stage - no actions performed'
                }
            }
        }
        stage('Release') {
            steps {
                script {
                    echo 'Release stage - no actions performed'
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
