pipeline {
    agent any

    stages {
        stage('Clonar y ejecutar script') {
            steps {
                git 'https://github.com/MarianoGarfel/jenkins-test.git'
                sh './script.sh'
            }
        }
    }
}