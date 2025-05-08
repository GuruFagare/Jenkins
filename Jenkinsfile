pipeline {
    agent any

    environment {
        DEPLOY_PATH = '/var/www/html'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/GuruFagare/Jenkins.git'
            }
        }

        stage('Deploy to Nginx') {
            steps {
                script {
                    // Ensure deployment directory exists and copy HTML file
                    sh """
                    sudo rm -rf ${DEPLOY_PATH}/*
                    sudo cp index.html ${DEPLOY_PATH}/
                    """
                }
            }
        }

        stage('Restart Nginx') {
            steps {
                sh 'sudo systemctl restart nginx'
            }
        }
    }

    post {
        success {
            echo 'Website deployed successfully!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}

