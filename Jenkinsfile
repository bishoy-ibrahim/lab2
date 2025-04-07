pipeline {
  agent any

  environment {
    TF_VAR_region = 'us-east-1'
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/bishoy-ibrahim/lab2.git'
      }
    }

    stage('Terraform Init') {
      steps {
        script {
          docker.image('hashicorp/terraform:light').inside('-v $PWD:/workspace -w /workspace') {
            sh 'terraform init'
          }
        }
      }
    }

    stage('Terraform Apply') {
      steps {
        script {
          docker.image('hashicorp/terraform:light').inside('-v $PWD:/workspace -w /workspace') {
            sh 'terraform apply -auto-approve'
          }
        }
      }
    }

    stage('Update Inventory') {
      steps {
        script {
          def ec2_ip = docker.image('hashicorp/terraform:light').inside('-v $PWD:/workspace -w /workspace') {
            sh(script: "terraform output -raw ec2_public_ip", returnStdout: true).trim()
          }
          writeFile file: 'inventory.ini', text: "[web]\n${ec2_ip} ansible_user=ec2-user ansible_ssh_private_key_file=~/.ssh/Key1.pem"
        }
      }
    }

    stage('Run Ansible') {
      steps {
        script {
          docker.image('willhallonline/ansible:latest').inside('-v $PWD:/ansible -w /ansible') {
            sh 'ansible-playbook -i inventory.ini playbook.yml'
          }
        }
      }
    }
  }
}
