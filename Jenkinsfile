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
                    if [ ! -f index.html ]; then
                      echo "ERROR: index.html not found"
                      exit 1
                    fi
                '''
            }
        }

        stage('Deploy to Nginx') {
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
            echo "✅ Deployment completed successfully"
        }
        failure {
            echo "❌ Deployment failed"
        }
    }
}
