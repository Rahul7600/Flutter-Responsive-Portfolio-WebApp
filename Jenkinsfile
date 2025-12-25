pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Flutter Web') {
            steps {
                sh '''
                    export PATH=$PATH:/opt/flutter/bin
                    flutter --version
                    flutter clean
                    flutter pub get
                    flutter build web --release
                '''
            }
        }

        /*
        stage('Deploy to App Server') {
            steps {
                sshagent(credentials: ['EC2_SSH_KEY']) {
                    sh '''
                        scp -o StrictHostKeyChecking=no -r build/web/* ubuntu@APP_SERVER_IP:/var/www/html/
                    '''
                }
            }
        }
        */

    }
}
