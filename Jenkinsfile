pipeline {
  agent any

  environment {
    TF_VAR_region = 'us-east-1'
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/your/repo.git'
      }
    }

    stage('Terraform Init') {
      steps {
        sh 'terraform init'
      }
    }

    stage('Terraform Apply') {
      steps {
        sh 'terraform apply -auto-approve'
        sleep(time: 60, unit: "SECONDS")
      }
    }

    stage('Update Inventory') {
      steps {
        script {
          def ec2_ip = sh(script: "terraform output -raw ec2_public_ip", returnStdout: true).trim()
          writeFile file: 'inventory.ini', text: "[web]\n${ec2_ip} ansible_user=ec2-user ansible_ssh_private_key_file=~/.ssh/Key1.ppk"
        }
      }
    }

    stage('Run Ansible') {
      steps {
        sh 'ansible-playbook playbook.yml'
      }
    }
  }
}
