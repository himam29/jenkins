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
                        sh "pwd"
                    }
                }
            }  
          stage("Terraform Init") {
            steps {
                script {
                    sh 'terraform init'
                }
            }
          }
        stage("Terraform Plan") {
            steps {
                script {
                    sh 'terraform plan'
                }
            }
        }
         stage("Terraform Apply") {
            steps {
                script {
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
                script {
                    sh 'terraform destroy --auto-approve'
                }
            }
         }
    }
}
