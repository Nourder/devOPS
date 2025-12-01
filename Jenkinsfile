pipeline {
    agent any

    environment {
        IMAGE_NAME = "python-print-app:latest"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nourder/devOPS.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // حذف الحاوية القديمة إذا كانت موجودة
                    sh "docker rm -f python-print-app || true"

                    // تشغيل الحاوية الجديدة
                    sh "docker run --name python-print-app ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline انتهى بنجاح!'
        }
        failure {
            echo 'Pipeline فشل.'
        }
    }
}
