pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git url: 'https://github.com/MominaRizwan/Assignment2.git', branch: 'main'
            }
        }

        stage('Clean up CI container') {
            steps {
                sh '''
                    echo "Cleaning up existing CI container (if any)..."
                    docker rm -f ecommerce-app-ci || true
                '''
            }
        }

        stage('Build & Run CI Container') {
            steps {
                echo 'Building and starting container using docker-compose.ci.yml...'
                sh 'docker compose --project-name ecommerce_pipeline -f docker-compose.yml up -d --build'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Check logs for details.'
        }
    }
}
