pipeline {
    agent any

    environment {
        IMAGE_NAME = "python-print-app:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Supprime l'ancien workspace pour éviter les erreurs Git
                    deleteDir()
                    
                    // Clonage du repo depuis GitHub
                    // Si ton repo est privé, ajoute `credentialsId: 'github-cred'`
                    git branch: 'main', url: 'https://github.com/Nourder/devOPS.git'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Vérifie que Docker est disponible
                    def dockerExists = sh(script: 'docker version >/dev/null 2>&1 && echo "ok" || echo "nok"', returnStdout: true).trim()
                    if (dockerExists != "ok") {
                        error "Docker n'est pas disponible sur cet agent !"
                    }
                    
                    // Build de l'image Docker
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Supprime le conteneur existant si présent
                    sh "docker rm -f python-print-app || true"
                    
                    // Lancement du conteneur
                    sh "docker run -d --name python-print-app -p 5000:5000 ${IMAGE_NAME}"
                }
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
