pipeline {
    agent any

    environment {
        IMAGE_NAME = "python-print-app:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nourder/devOPS.git', credentialsId: 'GITHUB_CREDENTIALS_ID'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker version || echo "Docker non disponible sur cet agent"'
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run Container') {
            steps {
                sh "docker rm -f python-print-app || true"
                sh "docker run -d --name python-print-app -p 5000:5000 ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo 'Pipeline terminé avec succès !'
        }
        failure {
            echo 'Pipeline échoué.'
        }
    }
}
