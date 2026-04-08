
pipeline {
    agent any

    stages {

        stage('Clone Backend Code') {
            steps {
                git branch: 'main',
                    credentialsId: 'pat-creds',
                    url: 'https://github.com/peakyblinder0509/instagram-mern.git'
            }
        }

        stage('Clean Old Build') {
         steps {https://github.com/peakyblinder0509/instagram-mern
                        dir('instagram-mern-backend'){

                sh '''
                docker system prune -f || true
                '''
            }
        }
        }

        stage('Build Docker Image') {
            steps {
                                      dir('instagram-mern-backend'){

                sh '''
                docker build --no-cache -t instagram-mern-backend-app:latest .
                '''
            }
        }
        }
        stage('Stop Old Container') {
            steps {
                                      dir('instagram-mern-backend'){

                sh '''
                docker stop instagram-mern-backend || true
                docker rm instagram-mern-backend || true
                '''
            }
        }
        }
        stage('Run New Container') {
            steps {
                                      dir('instagram-mern-backend'){

                sh '''
                docker run -d \
                -p 3000:3000 \
                --name instagram-mern-backend \
                instagram-mern-backend-app:latest
                '''
            }
        }
        }
        stage('Check Container Logs') {
            steps {
                sh '''
                docker logs instagram-mern-backend --tail=50
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment Success 🚀"
        }
        failure {
            echo "❌ Build Failed  😢"
        }
    }
}
