pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/sreenivasulub191/html.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan'
            }
        }

        stage('Deploy (Terraform Apply)') {
            steps {
                withAWS(credentials: 'ab50f2f7-d269-494c-91a7-500affcc7e46', region: 'us-east-1') {
                    sh 'terraform apply -auto-approve'
                }
            }
        }

        stage('Output Website URL') {
            steps {
                sh 'terraform output'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed successfully.'
        }
    }
}
