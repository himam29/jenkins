pipeline {
    agent any
        stages {
            stage ("checkout from git") {
                steps {
                    git branch: 'main', url: 'https://github.com/himam29/jenkins.git'
                }
            }

          stage("Run Terraform") {
            steps {
                script {
                    bat 'terraform --version'
                }
            }
          }

          stage ("Terraform Init") {
                steps {
                    dir("${env.WORKSPACE}"){
                      withAWS(credentials: "AWSCLI", region: 'us-east-2')  {  
                        bat "terraform init"
                      }  
                    }
                }
            }  

        stage("Terraform Plan") {
            steps {
                withAWS(credentials: "AWSCLI", region: 'us-east-2') {
                    bat 'terraform plan'
                }
            }
        }
         stage("Terraform Apply") {
            steps {
                withAWS(credentials: "AWSCLI", region: 'us-east-2') {
                    bat 'terraform apply --auto-approve'
                }
            }
         }
        stage("Approve To Destroy") {
            steps {
                input message: "Approve to Destroy", ok: "Destroy"
            }
        
        }
       stage("Terraform Destroy") {
            steps {
                withAWS(credentials: "AWSCLI", region: 'us-east-2') {
                    bat 'terraform destroy --auto-approve'
                }
            }
         }
    }
}
