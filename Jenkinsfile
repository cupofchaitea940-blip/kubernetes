pipeline {
    agent any

    environment {
        ARM_CLIENT_ID       = credentials('azure-client-id')
        ARM_CLIENT_SECRET   = credentials('azure-client-secret')
        ARM_SUBSCRIPTION_ID = credentials('azure-subscription-id')
        ARM_TENANT_ID       = credentials('azure-tenant-id')
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/cupofchaitea940-blip/kubernetes'
            }
        }

        stage('Terraform Version') {
            steps {
                bat 'terraform version'
            }
        }

        stage('Terraform Init') {
            steps {
                bat 'terraform init'
            }
        }

        stage('Terraform Validate') {
            steps {
                bat 'terraform validate'
            }
        }

        stage('Terraform Plan') {
            steps {
                bat 'terraform plan -var-file="terraform.tfvars"'
            }
        }

        stage('Terraform Apply') {
            steps {
                bat 'terraform apply -auto-approve -var-file="terraform.tfvars"'
            }
        }
    }

    post {
        success {
            echo 'AKS Cluster deployed successfully'
        }

        failure {
            echo 'Deployment failed'
        }
    }
}
