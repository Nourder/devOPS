pipeline {
    agent any                       // استخدام أي عامل (Agent) متاح
    environment {
        IMAGE_NAME = "python-print-app:latest"   // اسم الصورة التي سيتم إنشاؤها
    }
    stages {
        stage('Checkout') {          // المرحلة 1: استرجاع الكود
            steps {
           git branch: 'main', url: 
               'https://github.com/Nourder/devOPS.git'
            }
        }
        stage('Build Docker Image') {  // المرحلة 2: بناء صورة Docker
            steps {
                script {
                    docker.build("${IMAGE_NAME}")  // بناء الصورة بالاسم المحدد
                }
            }
        }
        stage('Run Container') {      // المرحلة 3: تشغيل الحاوية
            steps {
                script {
                    // إزالة أي حاوية قديمة بنفس الاسم
                    sh 'docker rm -f python-print-app || true'
                    // تشغيل الحاوية الجديدة
                    sh 'docker run --name python-print-app ${IMAGE_NAME}'
                }
            }
        }
    }
    post {                          // بعد انتهاء الـ Pipeline
        success {
            echo 'Pipeline انتهى بنجاح!'    // رسالة نجاح
        }
        failure {
            echo 'Pipeline فشل.'            // رسالة فشل
        }
    }
}
