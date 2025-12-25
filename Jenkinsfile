pipeline {
    agent any

    environment {
        APP_SERVER_IP = "34.231.70.226"
    }

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

        stage('Deploy to App Server') {
            steps {
                sshagent(credentials: ['EC2_SSH_KEY']) {
                    sh '''
                        rsync -avz --delete \
                        build/web/ ubuntu@$APP_SERVER_IP:/var/www/html/
                    '''
                }
            }
        }
    }
}
