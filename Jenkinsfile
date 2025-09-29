pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo '🔨 Construyendo el proyecto...'
                sh 'chmod +x script.sh'
                sh './script.sh'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Ejecutando pruebas...'
                sh 'echo "Test OK ✅"'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Desplegando la aplicación...'
                sh 'echo "Deploy completado ✅"'
            }
        }
    }

    post {
        always {
            echo '📜 Pipeline finalizado'
        }
    }
}
