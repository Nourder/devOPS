pipeline {
    agent any

    environment {
        IMAGE_NAME = "python-print-app:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Nourder/devOPS.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker rm -f python-print-app || exit 0'
                bat 'docker run -d --name python-print-app -p 5000:5000 %IMAGE_NAME%'
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
