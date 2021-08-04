pipeline {
environment {
        AWS_ACCESS_KEY_ID     = credentials('ABI_ACCESS_KEY')
        AWS_SECRET_ACCESS_KEY = credentials('ABI_SECRECT_KEY')
        AWS_DEFAULT_REGION = "us-east-1"
    }
agent  any
stages {
        stage('checkout') {
            steps {
                 script{

                        
                            git "https://github.com/Abishek-Ravichander/Terraform-Chef.git"
                        
                    }
                }
            }
        stage('AWS Connection Check') {
            steps {
                        sh '''
                        aws --version
                        aws ec2 describe-instances
                        '''
                }
            }
        
        stage('Plan') {
            steps {
                bat 'cd&cd terraform/Terraform-Chef & terraform init -input=false'
                bat 'cd&cd terraform/Terraform-Chef & terraform workspace new terraform || terraform workspace delete terraform'
                bat 'cd&cd terraform/Terraform-Chef & terraform workspace select terraform || terraform workspace new terraform'
                bat "cd&cd terraform/Terraform-Chef & terraform plan -input=false -out tfplan "
                bat 'cd&cd terraform/Terraform-Chef & terraform show -no-color tfplan > tfplan.txt'
            }
        }
       

        
        
        }
   }
