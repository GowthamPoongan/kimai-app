pipeline {
    agent any

    stages {
        stage('Clone Repo and Start Kimai') {
            steps {
                sh '''
                echo "[INFO] Cloning repo..."
                git clone https://github.com/GowthamPoongan/kimai-app.git /tmp/kimai-app

                echo "[INFO] Starting Docker containers..."
                docker compose -f /tmp/kimai-app/docker-compose.yml down || true
                docker compose -f /tmp/kimai-app/docker-compose.yml up -d
                '''
            }
        }

        stage('Check Docker Containers') {
            steps {
                sh 'docker ps'
            }
        }

        stage('Show App URL') {
            steps {
                script {
                    def ip = sh(script: "curl -s http://checkip.amazonaws.com", returnStdout: true).trim()
                    echo "🌐 Kimai App running at: http://${ip}:8001"
                }
            }
        }
    }
}
