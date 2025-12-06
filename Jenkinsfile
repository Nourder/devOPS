pipeline {
    agent any
    environment {
        IMAGE_NAME = "python-print-app:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                // Supprime workspace avant le clone
                deleteDir()
                // Clone GitHub (ajoute credentialsId si repo privé)
                git branch: 'main', url: 'https://github.com/Nourder/devOPS.git'
            }
        }

        stage('Build Docker Image') {
            steps {
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
