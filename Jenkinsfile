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
                        echo "[INFO] Stopping any previous containers (if exist)..."
                        docker compose -f /home/ec2-user/kimai-app/docker-compose.yml down || true

                        echo "[INFO] Starting Kimai and MySQL containers..."
                        docker compose -f /home/ec2-user/kimai-app/docker-compose.yml up -d
                    '''
                }
            }
        }

        stage('Verify Containers') {
            steps {
                sh 'docker ps'
            }
        }

        stage('Display Kimai URL') {
            steps {
                script {
                    def ip = sh(script: "curl -s http://checkip.amazonaws.com", returnStdout: true).trim()
                    echo "🌐 Access your Kimai app at: http://${ip}:8001"
                }
            }
        }

        stage('Check Jenkins Memory') {
            steps {
                sh 'free -h'
            }
        }
    }
}
