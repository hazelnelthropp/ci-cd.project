pipeline {
  agent any

  stages {
    stage('CheckOut') {
      steps {
        echo 'Checkout the source code from GitHub'
        git 'https://github.com/hazelnelthropp/ci-cd.project.git'
      }
    }

    stage('Docker Image Creation') {
      steps {
        sh 'docker build -t kranthi619/Hazel-pro:v1 .'
      }
    }

    stage('Docker Login') {
       steps {
                sh 'docker login -u kranthi619 -p Kranthi123#'
                sh 'docker push kranthi619/Hazel-pro:v1'
        }
      }
    }

    stage('Push Image to DockerHub') {
      steps {
        sh 'docker push kranthi619/Hazel-pro:v1'
      }
    }

    stage('Deploy Application Ansible') {
      steps { 
        ansiblePlaybook credentialsId: 'privatekey', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'deploy.yaml'
      }
    }
  }
}
