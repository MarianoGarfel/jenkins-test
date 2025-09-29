pipeline {
    agent any

    stages {
        stage('Clonar y ejecutar script') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/MarianoGarfel/jenkins-test.git']]
                ])
                sh './script.sh'
            }
        }
    }
}