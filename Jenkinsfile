pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = 'kimai'
    }

    stages {
        stage('Start Kimai with Docker Compose') {
            steps {
                script {
                    sh '''
                        echo "[INFO] Stopping any previous containers..."
                        docker-compose down || true

                        echo "[INFO] Starting Kimai and MySQL containers..."
                        docker-compose up -d
                    '''
                }
            }
        }

        stage('Verify Containers') {
            steps {
                sh 'docker ps'
            }
        }

        stage('Display App URL') {
            steps {
                script {
                    def ip = sh(script: "curl -s http://checkip.amazonaws.com", returnStdout: true).trim()
                    echo "🌐 Access your Kimai app at: http://${ip}:8001"
                }
            }
        }
    }
}
