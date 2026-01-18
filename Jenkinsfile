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

        stage('Validate Files') {
            steps {
                sh '''
                    set -e
                    test -f index.html
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    set -e
                    sudo rm -rf ${WEB_ROOT}/*
                    sudo cp -r . ${WEB_ROOT}/
                    sudo chown -R www-data:www-data ${WEB_ROOT}
                    sudo chmod -R 755 ${WEB_ROOT}
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful"
        }
        failure {
            echo "❌ Deployment failed"
        }
    }
}
