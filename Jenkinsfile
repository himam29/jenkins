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
                    sh 'terraform --version'
                }
            }
          }

          stage ("switch the directory") {
                steps {
                    dir("${env.WORKSPACE}"){
                        bat "terraform init"
                    }
                }
            }  
          stage("Terraform Init") {
            steps {
                dir("${env.WORKSPACE}"){
                    bat 'terraform init'
                }
            }
          }
        stage("Terraform Plan") {
            steps {
                dir("${env.WORKSPACE}"){
                    bat 'terraform plan'
                }
            }
        }
         stage("Terraform Apply") {
            steps {
                dir("${env.WORKSPACE}"){
                    sh 'terraform apply --auto-approve'
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
                dir("${env.WORKSPACE}"){
                    bat 'terraform destroy --auto-approve'
                }
            }
         }
    }
}
