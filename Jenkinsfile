pipeline {
    agent any

    environment {
        WEB_ROOT = "/var/www/html"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Validate Application') {
            steps {
                sh '''
                    set -e
                    test -f index.html
                '''
            }
        }

        stage('Prepare Web Root') {
            steps {
                sh '''
                    set -e
                    mkdir -p ${WEB_ROOT}
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    set -e
                    rm -rf ${WEB_ROOT}/*
                    cp -r . ${WEB_ROOT}/
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Web app deployed successfully"
        }
        failure {
            echo "❌ Deployment failed"
        }
    }
}
