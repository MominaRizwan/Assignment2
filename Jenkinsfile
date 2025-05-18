pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/MominaRizwan/Assignment2.git'
            }
        }

        stage('Create .env Files') {
            steps {
                script {
                    // backend/.env
                    writeFile file: 'backend/.env', text: """\
MONGODB_URI=mongodb+srv://faizankhurshid83:PVlzUOO1Dx0hH3W4@cluster0.7msvc.mongodb.net
CLOUDINARY_API_KEY=633795485598928
CLOUDINARY_SECRET_KEY=R0IwTeoVX25ofUCtOmCf2jUofhw
CLOUDINARY_NAME=drnbuwvjs
JWT_SECRET=ecommerce
ADMIN_EMAIL=admin@gmail.com
ADMIN_PASSWORD=admin1234

                    // frontend/.env
                    writeFile file: 'frontend/.env', text: """\
VITE_BACKEND_URL=http://54.145.158.79:4000
"""
                }
            }
        }

        stage('Build & Deploy with Docker Compose') {
            steps {
                script {
                    sh 'docker-compose -p ecommerce_ci down || true'
                    sh 'docker-compose -p ecommerce_ci build'
                    sh 'docker-compose -p ecommerce_ci up -d'
                }
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful!"
        }
        failure {
            echo "❌ Deployment failed."
        }
    }
}
