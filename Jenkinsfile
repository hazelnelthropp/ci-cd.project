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
        echo 'Building Docker images using Docker file'
        sh 'docker build -t kranthi619/Hazel-pro:v1 .'
      }
    }

    stage('Docker Login') {
       steps {
                echo 'Try to login to kranthi Docker hub'
                sh 'docker login -u kranthi619 -p Kranthi123#'
                sh 'docker push kranthi619/Hazel-pro:v1'
        }
      }
    }

    stage('Push Image to DockerHub') {
      steps {
        echo 'Try to push new image to kranthi Docker Hub'
        sh 'docker push kranthi619/Hazel-pro:v1'
      }
    }

    stage('Deploy Application Ansible') {
      steps { 
        echo 'Try to deploy Docker container in ec2 instance 5000 port'
        ansiblePlaybook credentialsId: 'ci-cd-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'deploy.yaml'
      }
    }
  }
}
