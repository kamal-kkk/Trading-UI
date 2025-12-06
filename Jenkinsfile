pipeline {
    agent any

    stages {

        stage('Git checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/betawins/Trading-UI.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                  echo "Installing dependencies..."
                  npm install
                '''
            }
        }

        stage('Build UI') {
            steps {
                sh '''
                  echo "Building Trading UI..."
                  npm run build || true
                '''
            }
        }

        stage('Start App with PM2') {
            steps {
                sh '''
                  pm2 delete Trading-UI || true
                  pm2 start npm --name Trading-UI -- start
                  pm2 save || true
                '''
            }
        }
    }

    post {
        success {
            echo "🎉 Trading UI Pipeline Completed Successfully!"
        }
        failure {
            echo "❌ Pipeline Failed — Check Logs"
        }
    }
}
