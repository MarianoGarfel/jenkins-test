pipeline {
    agent { label 'windows' } // Fuerza a usar tu Windows agent

    environment {
        AWS_ACCOUNT = 'XXxXXxXXxX' // Aquí se pondrá el AWS account real
    }

    parameters {
        choice(
            name: 'AWS_DEFAULT_REGION',
            description: 'Select the AWS region to deploy to',
            choices: ['us-east-1', 'us-west-2']
        )

        choice(
            name: 'ENVIRONMENT',
            description: 'Select the environment',
            choices: ['local', 'dev', 'prod']
        )
    }

    stages {
        stage("Build and Deploy Images") {
            steps {
                powershell """
                    Write-Host "========== Executing stage: Build Images =========="
                    aws ecr get-login-password --region ${params.AWS_DEFAULT_REGION} |
                        docker login --username AWS --password-stdin ${env.AWS_ACCOUNT}.dkr.ecr.${params.AWS_DEFAULT_REGION}.amazonaws.com

                    cd packager
                    pipenv run python --version
                    pipenv install --skip-lock --python 3.9

                    echo yes | pipenv run python package.py --all --account ${env.AWS_ACCOUNT} -e ${params.ENVIRONMENT}
                """
            }
        }

        stage("Build and Deploy Lambda Archives") {
            steps {
                powershell """
                    Write-Host "========== Executing stage: Build Lambda Archives =========="
                    cd packager
                    pipenv run python --version
                    pipenv install --skip-lock --python 3.9

                    echo yes | pipenv run python package_archive.py -e ${params.ENVIRONMENT}
                """
            }
        }
    }
}
