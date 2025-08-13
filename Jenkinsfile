pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key-id')     // Jenkins credential ID for AWS Access Key
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key') // Jenkins credential ID for AWS Secret Key
        AWS_DEFAULT_REGION    = 'us-east-2'                           // Ohio region
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo/terraform-ec2.git' // Replace with your repo URL containing main.tf & user_data
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Validate') {
            steps {
                sh 'terraform validate'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Terraform Apply') {
            steps {
                sh 'terraform apply -auto-approve tfplan'
            }
        }
    }

    post {
        success {
            echo "✅ Terraform deployment successful!"
        }
        failure {
            echo "❌ Terraform deployment failed!"
        }
    }
}
