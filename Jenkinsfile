pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git url: 'https://github.com/MominaRizwan/Assignment2.git', branch: 'main'
            }
        }

        stage('Clean Up Containers and Images') {
            steps {
                sh '''
                    echo "Stopping and removing old containers and images..."
                    docker rm -f frontend_ci_container_v2 backend_ci_container_v2 ecommerce-app-ci || true
                    docker rmi ecommerce_pipeline_frontend-ci ecommerce_pipeline_backend-ci || true
                    docker-compose -p ecommerce_pipeline -f docker-compose.yml down || true
                '''
            }
        }

        stage('Build & Run CI Containers') {
            steps {
                echo 'Building and starting containers using docker-compose.yml...'
                sh '''
                    docker-compose -p ecommerce_pipeline -f docker-compose.yml up -d --build
                '''
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
