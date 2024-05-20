pipeline {
  agent any

  stages {
    stage('CheckOut') {
      steps {
        echo 'Checkout the source code from GitHub'
        git 'https://github.com/kranthi619/kranthi-pro2.git'
      }
    }

    stage('Docker Image Creation') {
      steps {
        sh 'docker build -t kranthi619/finance-me .'
      }
    }

    stage('Docker Login') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'Docker-Hub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {         
          sh 'echo $dockerHubPassword | docker login -u $dockerHubUser --password-stdin'
        }
      }
    }

    stage('Push Image to DockerHub') {
      steps {
        sh 'docker push kranthi619/finance-me'
      }
    }

    stage('Deploy Application Ansible') {
      steps { 
        ansiblePlaybook credentialsId: 'privatekey', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'deploy.yml'
      }
    }
  }
}
